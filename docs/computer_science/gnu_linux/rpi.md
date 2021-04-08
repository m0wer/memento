---
title: Raspberry Pi
date: 2019-09-29
tags: [ 'rpi', 'raspberry pi' ]
---

# Raspberry Pi

## Guide

### Resize boot partition

The default boot partition size is sometimes not enough. In order to resize it,
we need to extract the SD/microSD card and plug it in on another device. Then
with `gparted`:

1. Move the **ext4** main data partition to the right, shrinking it if
   necessary.
1. Mount the boot **fat32** partition and copy its contents to your disk. E.g.
   `cp -r /media/sdc1/ /tmp/sdc1`.
1. Resize the boot partition and format it, because the `gparted` file system
   resize will fail due to the bug
   [649324](https://bugzilla.gnome.org/show_bug.cgi?id=649324).
1. Copy the contents back again to the newly formatted partition. E.g. `cp -r
   /tmp/sdc1/* /media/sdc1`.
1. Unmount the boot partition.

Everything should be ready now.

* [Raspberry Pi
  Forums](https://www.raspberrypi.org/forums/viewtopic.php?t=187999)

## Disable swap

To make your SD card live longer, you can reduce the number of reads and writes
by completely disabling swap.

```bash
sudo dphys-swapfile swapoff
sudo dphys-swapfile uninstall
sudo update-rc.d dphys-swapfile remove
```

* [Stopping SD Card Corruption on Raspberry Pi’s Raspbian – IdeaHeap](https://ideaheap.com/2013/07/stopping-sd-card-corruption-on-a-raspberry-pi/)
