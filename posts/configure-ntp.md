<!-- 
.. title: Configure NTP
.. slug: configure-ntp
.. date: 2013-01-01T00:00:08+02:00
.. tags: archlinux
.. link: 
.. description: 
.. type: text
-->

Install ntp:

```bash
# pacman -S ntp
```

Add the following lines in `/etc/ntp.conf`:

```
server 0.be.pool.ntp.org iburst
server 1.be.pool.ntp.org iburst
server 2.be.pool.ntp.org iburst
server 3.be.pool.ntp.org iburst
```

Enable ntpd at startup:

```bash
$ systemctl enable ntpd
```
