<!-- 
.. title: Configure i3bar and VPN pid
.. slug: configure-i3bar-and-vpn-pid
.. date: 2013-01-01T00:00:09+02:00
.. tags: archlinux, i3, openvpn
.. link: 
.. description: 
.. type: text
-->

In this case, I use the privatvpn script, which install the OpenVPN client.

Replace the command line in `/usr/bin/privatvpn` with:

```bash
/usr/sbin/openvpn --config /etc/openvpn/privatvpn.conf --writepid /var/run/openvpn.pid
```

Then point the .pid file in `~/.i3status.conf`, in `run_watch VPN`:

```
pidfile = "/var/run/openvpn.pid"
```
