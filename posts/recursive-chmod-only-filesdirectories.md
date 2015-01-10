<!-- 
.. title: Recursive chmod only files/directories
.. slug: recursive-chmod-only-filesdirectories
.. date: 2013-01-01T00:00:15+02:00
.. tags: archlinux
.. link: 
.. description: 
.. type: text
-->

Only files:

```console
$ find . -type f -exec chmod 644 {} \;
```

Only directories:

```console
$ find . -type d -exec chmod 755 {} \;
```
