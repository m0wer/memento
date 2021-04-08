---
title: 'APT: Debian package manager'
date: 2017-11-25
tags: [ 'apt', 'debian', 'package', 'manager' ]
---

# APT

## Debug

### Fix half-installed package

`apt install --reinstall [package]`

[askubuntu](https://askubuntu.com/questions/490671/fix-half-installed-package)

## Tips

```bash
alias uu='apt update && apt upgrade -y && apt-get autoremove -y'
```
