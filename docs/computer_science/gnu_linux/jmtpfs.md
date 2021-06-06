---
title: jmtpfs
date: 2021-06-06
author: m0wer
tags: [ 'android', 'mtp' ]
---

[`jmtpfs`](https://github.com/kiorky/jmtpfs) is a FUSE and libmtp based
filesystem for accessing MTP (Media Transfer Protocol) devices.

# Install

```bash
apt install jmtpfs
```
# Usage

Plug your Android device and enable file transfer, then from the computer:

```bash
jmtpfs {mountdir}
```
