<!-- 
.. title: Vim: export document to PDF
.. slug: vim-export-document-to-pdf
.. date: 2013-03-07T00:00:00+02:00
.. tags: archlinux, vim
.. link: 
.. description: 
.. type: text
-->

If you want your syntax highlight to be exported, don't forget to activate it
with:

```
:syntax on
```

Now print your document to PostScript:

```
:hardcopy > mydocument.ps
```

Exit Vim and use ps2pdf to convert mydocument.ps to mydocument.pdf.

```console
$ ps2pdf mydocument.ps
```
