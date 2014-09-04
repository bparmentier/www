<!-- 
.. title: Markdown linebreaks
.. slug: markdown-linebreaks
.. date: 2014-08-23T09:06:15+02:00
.. tags: markdown, syntax
.. link: 
.. description: 
.. type: text
-->

Adding a simple linebreak in Markdown is definitely not intuitive.
When you write:

```
Roses are red
Violets are blue
```

It will render:

> Roses are red
> Violets are blue

If you write a newline between the two:

```
Roses are red

Violets are blue
```

It will render two paragraphs:

> Roses are red  
>
> Violets are blue

The thing is to put two blank spaces at the end of the first line:

```latex
Roses are red␣␣
Violets are blue
```

It will then render:

> Roses are red  
> Violets are blue
