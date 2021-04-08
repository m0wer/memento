---
title: sysctl fixes and improvements
date: 2018-01-16
tags: [ 'sysctl', 'bug', 'error', 'fix', 'solution' ]
---

# sysctl

## Debug

### Computer freezing on almost full RAM

SWAP needs to be used before. Try to set the minimun free RAM values to a 5-6%
of the full memory by core.

`sysctl -w vm.min_free_kbytes=121268` 6% of 8GB multiplied by 4 cores

Also:

`sysctl -w vm.swappiness=5` Values from 0 to 100, being 0 only using SWAP if
absolutely necessary.

**Note:** Write this changes in */etc/sysctl.conf* to make them permanent.

[askubuntu](https://askubuntu.com/questions/41778/computer-freezing-on-almost-full-ram-possibly-disk-cache-problem)
