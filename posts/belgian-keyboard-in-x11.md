<!-- 
.. title: Belgian keyboard in X11
.. slug: belgian-keyboard-in-x11
.. date: 01/01/2013 00:00:00 AM UTC+02:00
.. tags: archlinux
.. link: 
.. description: 
.. type: text
-->

Create a `10-keyboard.conf` file in `/etc/X11/xorg.conf.d/` and add the following
lines:

```
Section "InputClass"
    Identifier          "Keyboard Defaults"
    MatchIsKeyboard     "yes"
    Option              "XkbLayout" "be(azerty)"
EndSection
```
