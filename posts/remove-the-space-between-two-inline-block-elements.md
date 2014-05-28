<!-- 
.. title: Remove the space between two inline-block elements
.. slug: remove-the-space-between-two-inline-block-elements
.. date: 01/01/2013 00:00:00 AM UTC+02:00
.. tags: web, html, css
.. link: http://css-tricks.com/fighting-the-space-between-inline-block-elements
.. description: 
.. type: text
-->

Using `display: inline-block` in your CSS file will leave a space between your elements.
Here is a trick to avoid this:

```html
<nav>
    <ul>
        <li><a href="#">Page1</a></li><!--
     --><li><a href="#">Page2</a></li><!--
     --><li><a href="#">Page3</a></li><!--
     --><li><a href="#">Page4</a></li>
    </ul>
</nav>
```

We add a blank comment between `</li>` and `<li>` to "fill" the space.
