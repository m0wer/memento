---
title: RXVT Unicode (urxvt)
date: 2017-10-29
tags: [ 'rxvt-unicode', 'shell', 'urxvt', 'ssh' ]
---

# RXVT Unicode (urxvt)

## Debug

### SSH: 'rxvt-unicode-256color': unknown terminal type

First create the directory to keep the terminfo file in the server:

`mkdir -p ~/.terminfo/r`

And then from the host:

`scp /usr/share/terminfo/r/rxvt-unicode-256color [server]:.terminfo/r`

[alemani](http://alemani.com/urxvt-unknown-terminal-type-with-ssh/)

It is a good idea to copy it directly to
*/usr/share/terminfo/r/rxvt-unicode-256color* in the remote server if possible.
