---
title: 'APT: Debian package manager'
date: 2017-11-25
tags: [ 'apt', 'debian', 'package', 'manager' ]
---

## Usage

### Install package from .deb

Either use `apt-get install ./{path to .deb}` or `dpkg -i {path to .deb}` and
then `apt-get -f install` if there are missing dependencies.

### List all installed packages and their versions

```bash
apt list --installed
```

## Debug

### Fix half-installed package

`apt install --reinstall [package]`

[askubuntu](https://askubuntu.com/questions/490671/fix-half-installed-package)

## Tips

```bash
alias uu='apt update && apt upgrade -y && apt-get autoremove -y'
```
