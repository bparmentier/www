<!-- 
.. title: Compose Key
.. slug: compose-key
.. date: 2014-12-25 21:40:12+01:00
.. tags: archlinux, keyboard
.. link: 
.. description: 
.. type: text
-->

The Compose Key allows you to input special characters by pressing two or more
subsequent keys. For example, pressing `Compose` then `/` + `=` will print a `≠`
(not equal to) sign.

Choose a key in the list:
```
grep "compose:" /usr/share/X11/xkb/rules/base.lst
```

Then add the following line in your `.xinitrc` (change `<key>` to the key you
want):
```
setxkbmap -option compose:<key>
```

Some useful combinations not directly accessible on my keyboard:
```
<Multi_key> <minus> <minus> <period>    : "–"   U2013 # EN DASH
<Multi_key> <minus> <minus> <minus>     : "—"   U2014 # EM DASH
<Multi_key> <period> <equal>            : "•"   enfilledcircbullet # BULLET
<Multi_key> <slash> <o>                 : "ø"   oslash # LATIN SMALL LETTER O WITH STROKE
<Multi_key> <o> <a>                     : "å"   aring # LATIN SMALL LETTER A WITH RING ABOVE
<Multi_key> <slash> <equal>  	        : "≠"   U2260 # NOT EQUAL TO
<Multi_key> <less> <equal> 	            : "≤"   U2264 # LESS-THAN OR EQUAL TO
<Multi_key> <greater> <equal> 	        : "≥"   U2265 # GREATER-THAN OR EQUAL TO
<Multi_key> <d> <i>		                : "⌀"   U2300 # DIAMETER SIGN
<Multi_key> <8> <8>                     : "∞"   U221e # 8 8 INFINITY
```

To configure the combinations:
```
cp /usr/share/X11/locale/en_US.UTF-8/Compose ~/.XCompose
```
