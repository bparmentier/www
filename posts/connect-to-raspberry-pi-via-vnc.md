<!-- 
.. title: Connect to Raspberry Pi via VNC
.. slug: connect-to-raspberry-pi-via-vnc
.. date: 2013-01-01T00:00:17+02:00
.. tags: archlinux, raspberry pi, vnc
.. link: 
.. description: 
.. type: text
-->

# Server side (Raspberry Pi running Raspbian)

Install tightvnc:

```bash
$ sudo apt-get install tightvncserver
```

Launch tightvnc with:

```bash
$ tightvncserver
```

It will ask you for a password and then show something like this:

```
New 'X' desktop is raspberrypi:1

Starting applications specified in /home/pi/.vnc/xstartup
Log file is /home/pi/.vnc/raspberrypi:1.log
```

Note the raspberrypi:1.

# Client side (my laptop running Arch Linux)

Install tightvnc:

```bash
# pacman -S tightvnc
```

Connect to your Raspberry Pi with (adapt your ip address):

```bash
$ vncviewer 192.168.1.4:1
```
