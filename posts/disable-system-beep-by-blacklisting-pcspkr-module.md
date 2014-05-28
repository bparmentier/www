<!-- 
.. title: Disable system beep (by blacklisting pcspkr module)
.. slug: disable-system-beep-by-blacklisting-pcspkr-module
.. date: 2013-01-01T00:00:01+02:00
.. tags: archlinux
.. link: 
.. description: 
.. type: text
-->

Create a `nobeep.conf` file in `/etc/modprobe.d/` and add the following line
(one per module):

```
blacklist pcspkr
```
