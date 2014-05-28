<!-- 
.. title: i3: force specific windows as always floating
.. slug: i3-force-specific-windows-as-always-floating
.. date: 2013-04-28T00:00:00+02:00
.. tags: archlinux, i3
.. link: 
.. description: 
.. type: text
-->

Sometimes you don't want i3 to open a window in tiling mode. This is generally
the case for popups or preference windows, like the one in Firefox (version 20).
While most of them are correctly handled by i3, some programs don't set the
right window type on those windows.

A way to fix it is to add a rule like this in your `~/.i3/config`:

```
for_window [class="Firefox" instance="Browser"] floating enable
```

To find out the class and instance of your window, launch xprop and click on it.

This will give you the window properties.

Look at the `WM_CLASS(STRING) = "Browser", "Firefox"`. The first one is the
instance and the second one is the class.
