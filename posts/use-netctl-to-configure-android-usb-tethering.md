<!-- 
.. title: Use Netctl to configure Android USB Tethering
.. slug: use-netctl-to-configure-android-usb-tethering
.. date: 2013-08-25T00:00:00+02:00
.. tags: archlinux, netctl
.. link: 
.. description: 
.. type: text
-->

Create a file named `usb-tether` in `/etc/netctl/` and add the following
configuration :

```
Description="A basic dhcp ethernet connection"
Interface=usb0
Connection=ethernet
IP=dhcp
```

Start the profile with:

```bash
# netctl start usb-tether
```

Or enable it with:

```bash
# netctl enable usb-tether
```
