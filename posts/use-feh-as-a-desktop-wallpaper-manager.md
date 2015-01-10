<!-- 
.. title: Use feh as a desktop wallpaper manager
.. slug: use-feh-as-a-desktop-wallpaper-manager
.. date: 2013-01-01T00:00:04+02:00
.. tags: archlinux
.. link: 
.. description: 
.. type: text
-->

```console
$ feh --bg-max image.png
```

This creates a `.fehbg` file in `$HOME`.

To restore the background on the next session, add the following line to the
startup file (`~/.xinitrc`):

```bash
eval $(cat ~/.fehbg) &
```
