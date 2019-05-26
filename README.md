dmenu_wifi
==========

This script provides a simple way to connect to wi-fi networks without the need for something like NetworkManager. There's a little bit of setup to get it working seamlessly:
 - This script was written for use with Arch Linux, so it uses `wpa_supplicant` and `dhcpcd`.
 - Make sure you have the `iw` utility installed to scan for and connect to networks.
 - This script uses the password patch for `dmenu`. It is available on the [Suckless website](https://tools.suckless.org/dmenu/patches/password/).
 - The script needs to know the name of your computer's wi-fi interface. It probably looks something like "wlp2s0" or "wlan0". Run `ip link` to list out all of your computer's network interfaces. Once you find it, set it as the value of `INTERFACE` in the script.
 - Because the commands the script uses have to talk directly to your computer's wi-fi hardware, many have to be run as root. This isn't the end of the world, but it's really inconvenient. Probably the best way around this is to carve out a [password exception](https://askubuntu.com/a/159009) for it in `/etc/sudoers`.

Other notes
-----------

 - When you tell `dmenu_wifi` to remember a wi-fi network, it will write a config file for it and store it in `/etc/wpa_supplicant/known_networks/`.
 - `dmenu_wifi` currently assumes that all networks require passwords. Testing on open networks has been limited and it is unknown whether it will work properly with such networks.
