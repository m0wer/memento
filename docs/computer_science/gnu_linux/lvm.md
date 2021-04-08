---
title: LVM
date: 2018-11-13
tags: [ 'linux', 'gnu', 'lvm', 'sys', 'disks', 'partitions' ]
---

# LVM

## Usage

### Display the physical volumes and the logical volumes they conatain

```bash
pvdisplay -m
```

[serverfault](https://serverfault.com/questions/461385/how-to-find-the-physical-volumes-that-hold-a-logical-volume-in-lvm#answer-461390)

### Create new physical volume

The device must have an empty partition table or if it's a partition, it should
have the **0x8e** identifier (for LVM). You can achieve this things with
`fdisk`. Once ready:

```bash
pvcreate [device]
```

[centos](https://www.centos.org/docs/5/html/Cluster_Logical_Volume_Manager/physvol_create.html)

### Move physical extents between physical volumes

This is useful if you want an already existing LV to be on a specific PV.

```bash
pvmove /dev/sda1:1000-1999 /dev/sdb1:0-999
```

[superuser](https://superuser.com/questions/435075/how-to-align-logical-volumes-on-contiguous-physical-extents#answer-700018)

### Create a logical volume

```bash
lvcreate -n [lv name] -L [size in gigabytes]g [vg name]
```

Then format it and mount it if requiered.

[debian wiki](https://wiki.debian.org/LVM#Create_an_LV)

### Extend LV and filesystem

To extend the logical volume and the filesystem in it use:

```bash
lvresize --resizefs --size +931GB /dev/vg/lv_home
```

When extending, the filesystem can be mounted, but not when shrinking.

* [systutorials](https://www.systutorials.com/5621/extending-a-mounted-ext4-file-system-on-lvm-in-linux/)

## Reference

* [redhat](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/logical_volume_manager_administration/)
