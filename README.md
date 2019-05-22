# pi-router
Simple setup and configuration tool for using a Raspberry Pi as a router

## Overview
This script was designed to easily setup a freshly installed Raspberry Pi
as a router.

Why you would want to do this is a bit dubious, as the device itself isn't
that great for the task.  This is more of just a proof of concept maybe,
or just for occasional use like a traveler that doesn't want to have to
reconfigure their devices every place they go.

I definitely **would not** suggest this in a production environment or
anywhere really where reliability is imnportant.  It works great for short
periods of time but will eventually trip over itself.

## Setup
First thing you need is obviously a Raspberry Pi with an SD Card.  You will
want to load the SD Card with some form of Raspbian.  I recommend the lite
edition unless you plan on using this for more than just a router.  Other
distros may work but as this relies on APT for package installation you may
have to make modifications to have it work with other flavors of Linux.

Once you have Raspbian loaded on the SD Card but before you load the card
into the Pi, make sure you place an empty file named `ssh` in the boot
partition.  This enables SSH access without having to first run `raspi-config`.

Put the SD Card in the Pi, connect it to an ethernet cable that is connected
to your network and plug in the power source to the Pi.

Give the pi a few seconds to come up and then you should be able to SSH into
it (pi@raspberrypi, default password is `raspberry`).

Of course run `sudo apt update` and `sudo apt upgrade` to update all the packages
to the current versions, and then run `sudo raspi-config` to tweak your Pi
to the specifications you wish.

Then lastly, you just run
> `wget https://raw.github.com/portablepirate/pi-router/pi-router`
and set it to executable with `chmod +x pi-router`

## Usage
`pi-router --wan interface --lan --interface [options]`

`-w | --wan interface` The name of the interface to use for the WAN, i.e. eth0
	or wlan0

`-l | --lan interface` The name of the interface to use for the LAN, i.e. eth0
	or wlan0

`-ds | --dhcp-start address` Starting IP address of the DHCP pool
	_Default is 10.13.37.50_

`-de | --dhcp-end address` Ending IP address of the DHCP pool
	_Default is 10.13.37.150_

`-swi | --static-wan-ip address` Set the WAN IP to the specified address
	_Default is DHCP obtained_

`-ri | --router-ip address` Set the router's IP address for the LAN side
	_Default is 10.13.37.1_

`-sub | --subnet-mask mask` Set the subnet mask of the LAN
	_Default is 255.255.255.0_

`-v | --version` Displays the version number of this script

`-h | --help` Displays the usage syntax

`-e | --essid name` Sets the ESSID name of the access point
	_Default is pi-router_

`-k | --wpa-psk key` Sets the shared ket for WPA authentication
	_Default is portablepirate_

`-c | --channel #` Sets the channel number for the wireless radio
	_Default is 4_

`--new-install` Does the initial setup for the script, including modifying
	system files

`-d | --dns host-list` Sets the DNS servers assigned to the DHCP clients via
	a comma separated list
	_Default is 8.8.8.8,8.8.4.4,10.13.37.1_

`--open-wifi` Configures hostapd to use an unsecured AP. **NOT RECOMMENDED**

`--no-wifi` Skips the WiFi configuration. Useful if you are routing between
	the onboard NIC and a USB ethernet dongle

## Changelog

Version 0.1
- Initial release
- Minimal testing with Raspbian Lite 4.14.  Please shoot me an email if you have got it to work with other distros/versions (portablepirate@gmail.com)

## Final Notes

This is part of my ongoing experimentation with Raspberry Pis.  If you have
any ideas that might work well with this project or just have a Pi project of
your own I'd love to hear about it!
