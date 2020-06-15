dmenu_wifi
==========

This script is meant to provide a simple way to connect to wi-fi networks
without the need for something like NetworkManager. It's precise
mechanisms for doing this are outlined in the comments at the top of
the script. There is a little bit of setup to get it working seamlessly:

- First, compatibility. This script assumes a system that has/uses
`wpa_supplicant`, `iw`, and `dhcpcd`. All of these are pretty
common packages, but some minimal distributions may not ship with
all of them. Additionally, a build of dmenu with the [password
patch](https://tools.suckless.org/dmenu/patches/password/) is required.
- To make the calls to `wpa_supplicant` and `iw`, the script has to be
provided with the name of your computer's wi-fi device. To find this,
run `ip link` to list out all of your network devices. The one you're
looking for probably looks something like "wlp2s0" or "wlan0". Once you
find it, set it as the value of `DEVICE` at the top of the script.
- Because the wi-fi commands used in the script have to talk directly to
the hardward, many have to be run as root. If there's a clean fix for this
using a udev rule or something, I haven't found it. My preferred solution
at the moment is to set the whole script to require root privileges,
then carve out a [password exception](https://askubuntu.com/a/159009)
for it in `/etc/sudoers`.

Other notes
-----------

- When you tell `dmenu_wifi` to remember a wi-fi network, it will write a
config file for it and store it in `/etc/wpa_supplicant/known_networks/`.
- `dmenu_wifi` currently does not have any way of knowing on its own
whether a network requires a password, so it will prompt you to tell it
whether to collect one or not whenever you connect to a new network.
