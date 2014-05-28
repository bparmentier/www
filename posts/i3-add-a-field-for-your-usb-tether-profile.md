<!-- 
.. title: i3: add a field for your usb-tether profile
.. slug: i3-add-a-field-for-your-usb-tether-profile
.. date: 2013-01-01T00:00:20+02:00
.. tags: archlinux, i3
.. link: 
.. description: 
.. type: text
-->

Add the following lines in your `~/.i3status.conf`:

```
ethernet usb0 {
    format_up = "U: %ip"
    format_down = "U: down"
}
```

And:

```
order += "ethernet usb0"
```

Restart i3 with `$MOD` + `Shift` + `R` (preserves your layout/session).
