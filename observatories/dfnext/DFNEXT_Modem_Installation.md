---
title: "DFNEXT Modem Installation"
parent: "DFNEXT"
grand_parent: "Observatories"
---
***Note: these instructions are for DFN camera systems equipped with
blue PCB modem adaptor board (see images below). For DFN observatories
with green PCB modem adaptor board please refer to [DFN Modem
Installation - Green
card]({{ site.baseurl }}{% link observatories/dfnext/DFN_Modem_Installation_-_Green_card.md %}).***

The DFNEXT observatories usually ship without modems as many of them are
deployed with WiFi or Ethernet connectivity and different areas of the
world require different modems.

If you wish to network your DFNEXT observatory via mobile broadband
instead of WiFi or Ethernet you need to source a modem and request a
modem installation care package from [DFN Camera
Help]({{ site.baseurl }}{% link Getting_Help.md %}). You will also need a 2FF ("standard")
sized SIM with an active data plan.

The recommended modems are the [Sierra Wireless AirPrime MC
Series](https://www.sierrawireless.com/-/media/iot/pdf/datasheets/sierrawireless_airprime_mc_series_datasheet.pdf)
MC7455 (for the Americas, Europe, the Middle East and Africa) and the
MC7430 (for Asia Pacific including Australia). It is also a good idea to
verify that the selected modem will support the frequencies/bands used
by your operator in the area.

# Installation Steps

Once you have the modem, installation care package (containing the modem
adaptor board, USB cable, modem bracket and screws) and a SIM card, you
can install the modem by following the steps bellow.
![Modem_cable_connector.jpg]({{ site.baseurl }}/images/Modem_cable_connector.jpg)
![Insert_modem.jpg]({{ site.baseurl }}/images/Insert_modem.jpg)
![Fasten_modem.jpg]({{ site.baseurl }}/images/Fasten_modem.jpg)
![Insert_sim.jpg]({{ site.baseurl }}/images/Insert_sim.jpg)
![Modem_bracket.jpg]({{ site.baseurl }}/images/Modem_bracket.jpg)
![Screw_in_modem_bracket.jpg]({{ site.baseurl }}/images/Screw_in_modem_bracket.jpg)
![Slide_bracket_to_the_right.jpg]({{ site.baseurl }}/images/Slide_bracket_to_the_right.jpg)
![Bend_usb_cable_using_hot_air_gun.jpg]({{ site.baseurl }}/images/Bend_usb_cable_using_hot_air_gun.jpg)
![Install_modem_with_connector_under_pcb.jpg]({{ site.baseurl }}/images/Install_modem_with_connector_under_pcb.jpg)
![Installed_modem.jpg]({{ site.baseurl }}/images/Installed_modem.jpg)
![Attach_gsm_antenna_pigtail_to_main_antenna_port.jpg]({{ site.baseurl }}/images/Attach_gsm_antenna_pigtail_to_main_antenna_port.jpg)
![Rf_cable_connected.jpg]({{ site.baseurl }}/images/Rf_cable_connected.jpg)
![Connect_usb_cable_to_pc.jpg]({{ site.baseurl }}/images/Connect_usb_cable_to_pc.jpg)
![Connected_usb_cables.jpg]({{ site.baseurl }}/images/Connected_usb_cables.jpg)

# Network configuration

Make sure the networking is configured correctly for a specific modem
type and operator. Please contact your service provider for details like
AP name (example: "telstra.m2m" for Australian Telstra M2M plans),
Password, Username and Phone (number) to dial.

The [Mobile network
configuration]({{ site.baseurl }}{% link network/Mobile_network_configuration.md %}) in the
observatory PC operating system has moved to a separate wiki page.