BBB Accesspoint
===============

TODO: write this so other people can understand it.

Given a wireless adapter wlan0 with 

Add /etc/udhcpd.conf from this repo.

in `/etc/network/interfaces` add:

	iface wlan0 inet static
	address 192.168.0.1
	netmask 255.255.255.0

Install necessary software (udhcpd should already be installed):

`$ sudo apt-get install hostapd`

Add /etc/hostapd/hostapd.conf from this repo.

Add the line `DAEMON_CONF="/etc/hostapd/hostapd.conf"` to `/etc/default/hostapd`.

Add it to autostart via

`$ sudo update-rc.d hostapd enable`

Add `net.ipv4.ip_forward=1` to `/etc/sysctl.conf`.


Add NAT rules to firewall:

	$ sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
	$ sudo iptables -A FORWARD -i eth0 -o wlan0 -m state --state RELATED,ESTABLISHED -j ACCEPT
	$ sudo iptables -A FORWARD -i wlan0 -o eth0 -j ACCEPT

And integrate it into bootup.

Reboot, ???? and profit.
