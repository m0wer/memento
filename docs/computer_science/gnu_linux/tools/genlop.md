---
title: genlop (portage)
date: 2018-01-18
tags: [ 'portage', 'gentoo', 'updates', 'packages', 'compile', 'estimate', 'eta', 'usage', 'reference', 'options' ]
---

# genlop (portage)

## Usage

### Estimate time of current ebuild

`emerge -ciq`

* `-c`: Display the currently compiling packages.
* `-i`: Extra infos for the selected package.
* `-q`: Query gentoo.linuxhowtos.org database if no local emerge was found.

### Estimate time of current emerge queue

`emerge --resume -p | genlop -p`

## Reference

* [gentoo-wiki](https://wiki.gentoo.org/wiki/Genlop)
