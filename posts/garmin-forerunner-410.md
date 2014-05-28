<!-- 
.. title: Garmin Forerunner 410
.. slug: garmin-forerunner-410
.. date: 2013-07-27T00:00:00+02:00
.. tags: archlinux, garmin, ant
.. link: 
.. description: 
.. type: text
-->

Install pyusb10 from AUR:

```bash
$ yaourt -S pyusb10
```

Install pip2:

```bash
$ sudo pacman -S python2-pip
```

Download python-ant-downloader from GitHub and install it:

```bash
$ git clone https://github.com/braiden/python-ant-downloader.git
```

```bash
$ cd python-ant-downloader
```

```bash
$ sudo pip2 install .
```

To access the USB device as a normal user, add the following line to
`/etc/udev/rules.d/99-garmin.rules`

```
SUBSYSTEM=="usb", ATTR{idVendor}=="0fcf", ATTR{idProduct}=="1008", MODE="666"
```

Launch ant-downloader.
```bash
$ ant-downloader
```

The first time it should ask for pairing: answer 'yes' on your GPS device.

Now you can set your preferences (like your Garmin Connect login and password)
in `~/.antd/antd.cfg`.
