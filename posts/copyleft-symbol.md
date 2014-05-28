<!-- 
.. title: Copyleft symbol
.. slug: copyleft-symbol
.. date: 08/13/2013 00:00:00 AM UTC+02:00
.. tags: web, html, css
.. link: 
.. description: 
.. type: text
-->

At this time there is no copyleft symbol in the Unicode character encoding standard. Some methods consist in using the copyright symbol and apply a symmetry on it. Here is how.

HTML:

```html
<p><span class="copyleft">&copy;</span> Copyleft ...</p>
```

CSS:

```css
.copyleft {
    display: inline-block;
    -moz-transform: scaleX(-1);
    -o-transform: scaleX(-1);
    -webkit-transform: scaleX(-1);
    transform: scaleX(-1);
    filter: FlipH;
    -ms-filter: "FlipH";
}
```

Note that I prefer writing *Copyleft* next to the symbol, because it is still semantically considered as a copyright one. Also, a lot of old browsers may not display it correctly.
