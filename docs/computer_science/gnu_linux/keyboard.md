---
title: Keyboard
date: 2021-04-26
author: m0wer
tags: [ 'keyboard', 'layout' ]
---

# Configuration

My favorite layout is [altgr-intl](https://altgr-weur.eu/altgr-intl.html)
because it is based on the standard US layout, which is comfortable for
programming and allows me to write accents on letters (required for Spanish
and French). And by adding some modifications it can be used for Turkish too.

![International keyboard (with AltGr dead keys](altgr-intl.gif)

To enable this layout, edit `/etc/default/keyboard` and add the following
content

```bash
# KEYBOARD CONFIGURATION FILE

# Consult the keyboard(5) manual page.

XKBMODEL="pc105"
XKBLAYOUT="us"
XKBVARIANT="intl"
XKBOPTIONS="caps:ctrl_modifier, shift:both_shiftlock"

BACKSPACE="guess"
```

With this you'll get the mentioned layout with some extra options, that make
the `Caps Lock` key behave as `Ctrl` and both `Shift` keys pressed at the same
time as `Caps Lock`.

Additionaly, the `Caps Lock` key (which is now mapped as `Ctrl`) can act as
`Esc` if pressed alone. To do so, install
[`xcape`](https://github.com/alols/xcape) and execute the following command

```bash
xcape -e 'Caps_Lock=Escape'
```

You can execute this command after login by adding it to your
`~/.config/i3/config` or in `~/.profile`.

## Turkish support

Turkish has a few letters that are not included by default in this layout, but
they can be added easily. We'll add the following mappings:

* ş: AltGr + s (and caps available with Shift)
* ğ: AltGr + g (and caps available with Shift)
* ı: AltGr + j
* İ: AltGr + Shift + j
* ç: AltGr + c (and caps available with Shift)

To add this mapping, create `~/.xmodmaprc` and add

```xmodmaprc
keycode  39 = s S s S scedilla Scedilla scedilla Scedilla
keycode  42 = g G g G gbreve Gbreve gbreve Gbreve
keycode  44 = j J j J idotless Iabovedot idotless Iabovedot
keycode  54 = c C c C ccedilla Ccedilla ccedilla Ccedilla
```

You can get the current mappings with

```bash
xmodmap -pke
```

Execute

```bash
xmodmap ~/.xmodmaprc
```

before the `xcode` command.
