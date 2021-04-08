---
title: smartmontools
date: 2019-07-24
tags: [ 'smartmontools', 'smartctl', 'sata', 'hdd' ]
---

# smartmontools

## Usage

### Understanding the exit code

Check the manual for the exit code values interpretation. There is a code for
understanding the mask.

## Debug

### Long test won't finish on a external drive

If you are getting `Interrupted (host reset)` in the selftest log it's probably
because you are using an external drive and the OS is stopping it after a
while. We need the disk to be active for the host all the time to avoid
suspension, to do so we can do:

```bash
sudo bash -c 'while true; do smartctl -a /dev/sdb > /dev/null; sleep 60; done'
```

* [StackExchange](https://superuser.com/questions/766943/smart-test-never-finishes)

## Reference

### General usage

* [gentoo wiki](https://wiki.gentoo.org/wiki/Smartmontools)
