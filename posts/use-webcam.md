<!-- 
.. title: Use webcam
.. slug: use-webcam
.. date: 2013-04-11T00:00:00+02:00
.. tags: archlinux, webcam
.. link: 
.. description: 
.. type: text
-->

Add yourself to the video group:

```console
# gpasswd -a <user> video
```

To use it with mplayer type the following command:

```console
$ mplayer tv:// -tv driver=v4l2:width=640:height=480:device=/dev/video0 -fps 15
```
