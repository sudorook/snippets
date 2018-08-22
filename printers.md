# Printers

## HP network printer

1. Install the cups, system-config-printer, and hplip packages on Arch Linux or
   their equivalents if using another distribution.
2. Run system-config-printer (as root). The CUPS systemd service needs to be
   running.
3. Select network printers from the side menu.
4. Enter the device IP address and search for possible protocols.
5. Select the option with the hp://net URI.
6. Select the device model from the list.


## Epson network printer

1. Install the cups and system-config-printer packages on Arch Linux or their
   equivalents if using another distribution.
2. Look up the device driver through the [Epson driver
   site](http://download.ebz.epson.net/dsc/search/01/search/?OSC=LX). For rpm-
   or deb-based distributions, find the corresponding files for your hardware
   architecture on the Epson driver website. For Arch Linux, look for the
   appropriate driver in the AUR or repackage the rpm file yourself.
3. Run system-config-printer (as root). The CUPS systemd service needs to be
   running.
4. Select network printers from the side menu.
5. Enter the device IP address and search for possible protocols.
6. Select the option with the hp://net URI.
7. Select the device model from the list.
