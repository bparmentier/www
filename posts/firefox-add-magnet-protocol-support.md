<!-- 
.. title: Firefox: add "magnet:" protocol support
.. slug: firefox-add-magnet-protocol-support
.. date: 2013-01-01T00:00:19+02:00
.. tags: archlinux, firefox, torrent
.. link: 
.. description: 
.. type: text
-->

Type `about:config` in your address bar.

Right-click → New → Boolean → Name: `network.protocol-handler.expose.magnet` →
Value → `false`.

Next time you use the magnet protocol, it will give you the "associate
application" box.

Point it to the `magnet2torrent` script below if you want to associate it with
rtorrent.
