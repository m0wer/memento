---
title: fdisk
date: 2017-10-10
tags: partition,USB,format,fdisk
---
# fdisk

## Create new partition: 

```bash
fdisk [disk]
n
# answer the questions
w # write changes
```

## Delete partitions

```bash
fdisk [device]
p # to list current partitions
d
w # write changes
```
