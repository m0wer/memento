---
title: mimeopen default applications
date: 2018-11-02
tags: [ 'miemopen', 'lis', 'default', 'applications', 'mimeapps', 'xdg' ]
---

# mimeopen default applications

## Usage

### Check the current default application

`mimeopen [file]` or `mimeopen .[extenesion]`.

### Change the default application

`mimeopen -d [file]` or `mimeopen -d .[extenesion]`.

`mimeopen` will change or add the entries to *~/.config/mimeapps.list*. If a
*.desktop* entry is requiered for some app, it will be automatically created in
*.local/share/applications/*.

[askubuntu](https://askubuntu.com/questions/90214/how-do-i-set-the-default-program)
