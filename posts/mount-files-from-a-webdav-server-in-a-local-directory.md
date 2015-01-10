<!-- 
.. title: Mount files from a WebDAV server in a local directory
.. slug: mount-files-from-a-webdav-server-in-a-local-directory
.. date: 2014-02-07T00:00:00+02:00
.. tags: archlinux, webdav
.. link: 
.. description: 
.. type: text
-->

If you have a server with Owncloud installed, you probably have access to it
through WebDAV. You can use the command line with
[cadaver](http://www.webdav.org/cadaver/) or mount it as a local directory with
[davfs2](https://savannah.nongnu.org/projects/davfs2).

The [Davfs article](https://wiki.archlinux.org/index.php/Davfs) on ArchWiki is
well explained:

Add yourself to the network group:

```console
# usermod -a -G network <user>
```

Restart your session, and add the following entry in `/etc/fstab`:

```text
https://owncloud.yourserver.com/remote.php/webdav/ /home/<user>/Owncloud davfs user,noauto,uid=,file_mode=600,dir_mode=700 0 1
```

Edit `~/.davfs/secrets` and add your credentials like this:

```
"https://owncloud.yourserver.com/remote.php/webdav/" "webdavuser" "webdavpassword"
```

Note that the double quotes are not required, but if your password contains
special characters, it may help.

Now you should be able to mount and unmount `~/Owncloud` with:

```console
$ mount ~/Owncloud
```

```console
$ fusermount -u ~/Owncloud
```
