<!-- 
.. title: Configure VirtualBox
.. slug: configure-virtualbox
.. date: 2013-01-01T00:00:06+02:00
.. tags: archlinux, virtualbox
.. link: 
.. description: 
.. type: text
-->

Install it with:

```console
# pacman -S virtualbox qt
```

Add user `bp` to the `vboxusers` group:

```console
# gpasswd -a bp vboxusers
```

Load kernel module at boot:

```console
# tee /etc/modules-load.d/virtualbox.conf <<< "vboxdrv"
```
