<!-- 
.. title: Properly remove DHCP lease file upon disconnection
.. slug: properly-remove-dhcp-lease-file-upon-disconnection
.. date: 2013-01-01T00:00:07+02:00
.. tags: archlinux
.. link: 
.. description: 
.. type: text
-->

Add the following line to `/etc/profile`:

```bash
PRE_UP=' [ -e /var/lib/dhcpcd/dhcpcd-wlan0.lease ] && rm /var/lib/dhcpcd/dhcpcd-wlan0.lease '
```
