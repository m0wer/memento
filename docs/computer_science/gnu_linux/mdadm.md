---
title: "mdadm: Linux software RAID"
date: 2018-11-13
tags: [ 'mdadm', 'linux', 'raid', 'software', 'sys' ]
---

# Usage

## Add RAID device to initramfs

1. Add the currently active RAID devices to *mdadm.conf*:
   `mdadm --detail --scan > /etc/mdadm/mdadm.conf`
1. Update the **initramfs**: `update-initramfs -u`

[serverfault](https://serverfault.com/questions/209379/what-tells-initramfs-or-the-ubuntu-server-boot-process-how-to-assemble-raid-arra'#answer-222729)

## Check the RAID devices status

```bash
cat /proc/mdstat
```

## RAID0

### Create RAID0 from one disk

If you have a regular disk without RAID, and you want to convert it to a RAID0
device so you can add more disks later, you can't do it directly. Instead
you'll have to:

1. Install the new disk to the machine and create a RAID0 array with only that
  drive.
1. Setup the partitions on it and copy the data from the original drive.
1. Change `/etc/crypttab` and `/etc/fstab` if needed to use the partition(s)
  of the RAID0 array.
1. Extend the RAID0 adding the original disk as instructed in the next section.

### Extend RAID0

1. Format the disk to be added generating a new partition table and a new
  partition. You can use `fdisk`.
1. Extend the existing RAID0 array with

  ```bash
  mdadm --grow /dev/mdX --raid-devices=2 --add /dev/sdXN
  ```

  This will convert the array to RAID4 temporarily since RAID0 can't be extended
  directly. You can check the reshape status with `cat /proc/mdadm`.
1. Resize the partitions, and everything needed.

# Reference

## Usage

* [ducea](http://www.ducea.com/2009/03/08/mdadm-cheat-sheet/)

## RAID1

### Setup

* [tecmint](https://www.tecmint.com/create-raid1-in-linux/)
