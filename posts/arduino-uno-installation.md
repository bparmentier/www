<!-- 
.. title: Arduino Uno installation
.. slug: arduino-uno-installation
.. date: 2013-03-15T00:00:00+02:00
.. tags: archlinux, arduino
.. link: 
.. description: 
.. type: text
-->

First install the arduino package from AUR:

```bash
$ sudo yaourt -S arduino
```

Add yourself to the `uucp` group:

```bash
$ sudo gpasswd -a <user> uucp
```

Logout and login again.

Connect your arduino to your computer and lauch:

```bash
$ ls /dev/ttyUSB* /dev/ttyACM*
```

Note the serial port of the board.

Launch the arduino program, close it, then modify `~/.arduino/preferences.txt`.

Change the line `serial.port=COM1` with something like this:

```
serial.port=/dev/ttyACM0
```

Lauch again the arduino program.

If you can't upload your sketch (and get the following error: `Serial port
'/dev/ttyACM0' not found. Did you select the right one from the Tools > Serial
Port menu?`), this may be because you don't have write permissions on
`/run/lock/` directory.

The following trick should resolve the problem:

```bash
$ sudo chmod 777 /run/lock
```

```bash
$ sudo cp /usr/lib/tmpfiles.d/legacy.conf /etc/tmpfiles.d/
```

```bash
$ sudo chmod 777 /etc/tmpfiles.d/legacy.conf
```
