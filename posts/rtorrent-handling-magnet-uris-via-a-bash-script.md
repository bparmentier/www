<!-- 
.. title: rtorrent: handling "magnet:" URIs via a bash script
.. slug: rtorrent-handling-magnet-uris-via-a-bash-script
.. date: 2013-01-01T00:00:18+02:00
.. tags: archlinux, torrent
.. link: http://wiki.rtorrent.org/MagnetUri
.. description: 
.. type: text
-->

Create a `magnet2torrent` script with the following code:

```bash
#! /bin/bash

# Convert a magnet URI into a .torrent file
# Run the script with:
# ./magnet2torrent.sh "MAGNET_URI"
# (Don't forget the quotes aroud MAGNET_URI)

cd ~/watch || exit    # set your watch directory here
[[ "$1" =~ xt=urn:btih:([^&/]+) ]] || exit
hashh=${BASH_REMATCH[1]}
if [[ "$1" =~ dn=([^&/]+) ]];then
    filename=${BASH_REMATCH[1]}
else
    filename=$hashh
fi
echo "d10:magnet-uri${#1}:${1}e" > "meta-$filename.torrent"
```

Make the script executable:

```bash
$ chmod a+x magnet2torrent
```

Run the script with a magnet URI (after adding it to your `$PATH` variable):

```bash
$ magnet2torrent "MAGNET_URI"
```
