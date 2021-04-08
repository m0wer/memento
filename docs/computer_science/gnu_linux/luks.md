---
title: LUKS usage
date: 2018-09-17
tags: [ 'luks', 'cryptsetup', 'encryption', 'cipher', 'device', 'disk', 'usb' ]
---

# LUKS

## Usage

### Setup ciphered disk with partitions

1. `cryptsetup -v --cipher aes-xts-plain64 --key-size 512 --hash sha512 --iter-time 5000 --use-random --verify-passphrase luksFormat [device]`
1. `cryptsetup luksOpen [device] [mountpoint_name]`
1. Create partitions and format.

[archlinux-wiki](https://wiki.archlinux.org/index.php/dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode)

## Reference

* [howtoforge](https://www.howtoforge.com/automatically-unlock-luks-encrypted-drives-with-a-keyfile) Automatically unlock LUKS drives.
* [How to Change Your LUKS Encryption Passphrase - Make Tech Easier](https://www.maketecheasier.com/change-luks-encryption-passphrase/)
