<!-- 
.. title: Optimize SSD Performance
.. slug: optimize-ssd-performance
.. date: 2013-01-01T00:00:21+02:00
.. tags: archlinux, ssd
.. link: https://wiki.archlinux.org/index.php/Solid_State_Drives
.. description: 
.. type: text
-->

# Enable TRIM

Warning: the following tip only works for Linux kernel version 2.6.33 or above,
and not all filesystems are supported (as of version 3.7, ext4, btrfs, JFS and
XFS support it).

Add the discard option in `/etc/fstab`.

Example:

```
/dev/sda1  /       ext4   defaults,noatime,discard   0  1
/dev/sda2  /home   ext4   defaults,noatime,discard   0  2
```
