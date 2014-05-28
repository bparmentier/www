<!-- 
.. title: Wi-Fi connection frequently drops
.. slug: wi-fi-connection-frequently-drops
.. date: 2013-01-01T00:00:12+02:00
.. tags: archlinux
.. link: 
.. description: 
.. type: text
-->

Create a iwlwifi.conf file in `/etc/modprobe.d/` containing the following line:

```
options iwlwifi 11n_disable=1 swcrypto=1
```
