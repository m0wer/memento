---
title: Linux kernel
date: 2018-11-02
tags: [ 'linux', 'GNU', 'kernel', 'tips', 'usage' ]
---

# Linux kernel

## Usage

### Load modules at boot

Add the desired modules in */etc/conf.d/modules*:

```
modules="[...]"
```

[supreuser](https://superuser.com/questions/901371/start-a-module-at-startup-on-gentoo)

## Tips

### Remove old kernels in gentoo

1. Remove the source directory: `rm -r /usr/src/linux-4.X.Y`.
2. Remove the modules: `rm -r /lib/modules/4.X.Y`.
3. Remove the files in */boot* coresponding to the old kernel. E.g: *vmlinuz*,
   *initramfs*, *kernel*, *config*, *initramfs*...

[gentoo-wiki](https://wiki.gentoo.org/wiki/Kernel/Removal)
