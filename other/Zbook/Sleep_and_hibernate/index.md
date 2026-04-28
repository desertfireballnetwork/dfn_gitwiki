---
title: "Zbook Sleep and Hibernate"
has_children: true
parent: "Other"
---

# Instructions to enable S4 hibernate on 2025 ZBook

This mode is also called "suspend to disk". It is supposed to have the lowest power consumption, pretty much same as S5 power down.

(Tested on: SBKPFV3 HP ZBook 8 G1i 14 inch Mobile Workstation PC)

## 1. Make sure there is swap partition or swap file
Ideally bigger than physical RAM. That is where the memory state will be saved as the RAM is not powered in S4 hiberbate.

```
swapon --show 

martin@mcu-zbook:~$ swapon --show
NAME           TYPE       SIZE USED PRIO
/dev/nvme0n1p3 partition 74.5G   0B   -2
```
If not, create swap partition or swap file - see Step 1 of the instructions (link at the bottom of this page)

### 1.1) Swap settings
I have plenty of RAM (64GB) and I like to reduce swapping to only necessary situations, so that there is ideally "always" enough space on swap for suspend to disk:
```
martin@mcu-zbook:~$ grep swappiness /etc/sysctl.conf  
vm.swappiness=1

cat /proc/sys/vm/swappiness  
1
```

### 1.2) make sure secure boot in BIOS is disabled - verify from linux console w/o reboot:
```
martin@mcu-zbook:~$ mokutil --sb-state
SecureBoot disabled
```

## 2) set  resume parameter for the grub bootloader - point it to swap partition/file
```
sudo emacs /etc/default/grub

...

GRUB_CMDLINE_LINUX_DEFAULT="quiet splash resume=/dev/nvme0n1p3"
...
```

## 3) Enable Hibernate option in Power-Off Menu

```
sudo mkdir -p /etc/polkit-1/localauthority/50-local.d
sudo apt install polkitd-pkla
```
create file /etc/polkit-1/localauthority/50-local.d/com.ubuntu.enable-hibernate.pkla

with the following content:
```
[Re-enable hibernate by default in upower]
Identity=unix-user:*
Action=org.freedesktop.upower.hibernate
ResultActive=yes

[Re-enable hibernate by default in logind]
Identity=unix-user:*
Action=org.freedesktop.login1.hibernate;org.freedesktop.login1.handle-hibernate-key;org.freedesktop.login1;org.freedesktop.login1.hibernate-multiple-sessions;org.freedesktop.login1.hibernate-ignore-inhibit
ResultActive=yes
```
or

create file /etc/polkit-1/rules.d/10-enable-hibernate.rules

with the following content:

```
polkit.addRule(function(action, subject) {
   if (action.id == "org.freedesktop.login1.hibernate" ||
       action.id == "org.freedesktop.login1.hibernate-multiple-sessions" ||
       action.id == "org.freedesktop.upower.hibernate" ||
       action.id == "org.freedesktop.login1.handle-hibernate-key" ||
       action.id == "org.freedesktop.login1.hibernate-ignore-inhibit")
   {
       return polkit.Result.YES;
   }
});
```

**(I did both, my desktop manager is Mate)

reboot

## 4) Test: 

Shutdown->hibernate menu item is there. Hibernate from menu works.

Commandline: (also from text console, eg Ctrl+Alt+F2)

```
sudo systemctl hibernate
```

Both works!

It takes quite long time though, both the hibernating and restoring, so be patient. The hibernating turns screens off shortly after initiating, then the go on again soon, which is confusing. Particularly because the mouse/keyb control is seemingly"frozen" until the laptop actually fully hibernates.

## 5) Celebrate! Play with extras... or troubleshoot

### 5.1) extras

In Control center -> Power Management -> On Battery Power, for "When battery power is critically low", set Hibernate.

Then the system should hibernate to disk, minimising the power consumption, rather than shutdown or hard crash running out of battery capacity.

---

#### Other useful tools, config and power related (optional)

dconf-editor

```
sudo apt install dconf-editor
sudo dconf-editor
```

TLP

```
sudo tlp star

sudo tlp-stat -s
sudo tlp-stat
```
config: /etc/tlp.conf

(https://www.fosslinux.com/135830/how-to-fine-tune-power-management-in-ubuntu-using-tlp.htm)

### 5.2) Issues 

External screen may be blank on resume. Fix: Switch that ext screen video output off in xrandr/display settings, then hit "restore previous configuration" to actually not switch it off.

## 6. Resources
https://ubuntuhandbook.org/index.php/2021/08/enable-hibernate-ubuntu-21-10/