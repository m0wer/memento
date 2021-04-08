---
title: Kali Linux
date: 2017-12-15
tags: [ 'kali', 'gnu', 'linux', 'pentesting' ]
---

# Kali Linux

## Install

### Live USB with encrypted persistence

Download an flash latest version from
[kali-downloads](https://www.kali.org/downloads/).

Then:

```bash
usb=/dev/sdc3
echo $usb # just in case...
parted /dev/sdb mkpart primary 3000 100%
cryptsetup --verbose --verify-passphrase luksFormat $usb
cryptsetup luksOpen $usb my_usb
mkfs.ext3 -L persistence $usb
e2label $usb persistence
mkdir -p /mnt/my_usb
mount /dev/mapper/my_usb /mnt/my_usb
echo "/ union" > /mnt/my_usb/persistence.conf
umount /dev/mapper/my_usb
cryptsetup luksClose /dev/mapper/my_usb
```

[kali-docs](https://docs.kali.org/downloading/kali-linux-live-usb-persistence)
