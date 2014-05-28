<!-- 
.. title: Multiple screens
.. slug: multiple-screens
.. date: 2013-03-21T00:00:00+02:00
.. tags: archlinux
.. link: 
.. description: 
.. type: text
-->

So, I have a laptop with a 1920\*1080 screen and I want to connect it with a
1680\*1050 LCD monitor through VGA.

First make sure xorg-xrandr is installed:

```bash
$ sudo pacman -S xorg-xrandr
```

Connect the monitor and run:

```bash
$ xrandr -q
```

Note the names of the two outputs, then run:

```bash
$ xrandr --output LVDS1 --pos 0x0 --mode 1920x1080 --output VGA1 --mode 1680x1050 --left-of LVDS1
```
