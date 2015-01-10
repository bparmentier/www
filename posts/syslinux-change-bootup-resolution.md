<!-- 
.. title: Syslinux: change bootup resolution
.. slug: syslinux-change-bootup-resolution
.. date: 2013-01-01T00:00:10+02:00
.. tags: archlinux, syslinux
.. link: 
.. description: 
.. type: text
-->

To know which resolutions are supported by your screen, install hwinfo:

```console
# pacman -S hwinfo
```

Then execute:

```console
# hwinfo --vbe | grep 'Mode '
```

Modes are displayed in hexadecimal.

Now edit `/boot/syslinux/syslinux.cfg` and add to the `APPEND` line the desired
resolution with:

```
vga=<resolution>
```

where `<resolution>` is the corresponding hexa code.

For example: add `vga=0x037f` if you want 1920x1080x24.
