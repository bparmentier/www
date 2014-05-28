<!-- 
.. title: Configure sudo
.. slug: configure-sudo
.. date: 2013-01-01T00:00:05+02:00
.. tags: archlinux
.. link: 
.. description: 
.. type: text
-->

Install with:

```bash
# pacman -S sudo
```

# Allow user `bp` to use sudo

Add the following line in section "User privilege specification:

```
bp ALL=(ALL) ALL
```

# Use Vim as default editor for visudo

Add the following lines to `/etc/sudoers`:

```
# Reset environment by default
Defaults      env_reset
# Set default EDITOR to vim, and do not allow visudo to use EDITOR/VISUAL.
Defaults      editor="/usr/bin/vim -p -X", !env_editor
```
