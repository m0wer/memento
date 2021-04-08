---
title: Linux software RAID
date: 2018-11-13
tags: [ 'mdadm', 'linux', 'raid', 'software', 'sys' ]
---

# mdadm: Linux software RAID

## Usage

### Add RAID device to initramfs

1. Add the currently active RAID devices to *mdadm.conf*:
   `mdadm --detail --scan > /etc/mdadm/mdadm.conf`
1. Update the **initramfs**: `update-initramfs -u`

[serverfault](https://serverfault.com/questions/209379/what-tells-initramfs-or-the-ubuntu-server-boot-process-how-to-assemble-raid-arra'#answer-222729)

### Check the RAID devices status

```bash
cat /proc/mdstat
```

## Reference

### Usage

* [ducea](http://www.ducea.com/2009/03/08/mdadm-cheat-sheet/)

### RAID1

#### Setup

* [tecmint](https://www.tecmint.com/create-raid1-in-linux/)
