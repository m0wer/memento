---
title: LUKS usage
date: 2018-09-17
tags: [ 'luks', 'cryptsetup', 'encryption', 'cipher', 'device', 'disk', 'usb' ]
---

# Usage

## Setup ciphered disk with partitions

1. `cryptsetup -v --cipher aes-xts-plain64 --key-size 512 --hash sha512 --iter-time 5000 --use-random --verify-passphrase luksFormat [device]`
1. `cryptsetup luksOpen [device] [mountpoint_name]`
1. Create partitions and format.

[archlinux-wiki](https://wiki.archlinux.org/index.php/dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode)

## Add a keyfile

First, create the keyfile with

```bash
dd bs=512 count=4 if=/dev/random of=/etc/mykeyfile iflag=fullblock
```

This will generate a keyfile of 2048 random bytes in the specified location.

Then, set the proper permissions with

```bash
chmod 600 /etc/mykeyfile
```

Then, add the keyfile to the LUKS header with

```bash
cryptsetup luksAddKey {luks_partitition} /etc/mykeyfile
```

## Change the passphrase

To change a passphrase of a LUKS device to another:

```bash
cryptsetup luksChangeKey {device}
```

You will be prompted for the old passphrase and the new one twice. The device
can be unlocked and in-use while changing the password.

# Reference

* [howtoforge](https://www.howtoforge.com/automatically-unlock-luks-encrypted-drives-with-a-keyfile) Automatically unlock LUKS drives.
* [How to Change Your LUKS Encryption Passphrase - Make Tech Easier](https://www.maketecheasier.com/change-luks-encryption-passphrase/)
