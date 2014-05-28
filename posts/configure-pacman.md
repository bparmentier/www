<!-- 
.. title: Configure pacman
.. slug: configure-pacman
.. date: 2013-01-01T00:00:11+02:00
.. tags: archlinux, pacman
.. link: 
.. description: 
.. type: text
-->

# Auto-completion

For advanced completion, install the bash-completion package:

```bash
# pacman -S bash-completion
```

# The "command not found" hook

Install pkgfile:

```bash
# pacman -S pkgfile
```

Then update the database with:

```bash
# pkgfile --update
```

Note: didn't work for me.

# Add color output

*EDIT: the following trick is not needed anymore since pacman (>= 4.1) now
supports color output.*

Install pacman-color from AUR.

Backup the original pacman executable:

```bash
# mv /usr/bin/pacman /usr/bin/pacman.bak
```

Make a symlink from pacman to pacman-color:

```bash
# ln -s /usr/bin/pacman-color /usr/bin/pacman
```
