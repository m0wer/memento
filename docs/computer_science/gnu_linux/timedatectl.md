---
title: timedatectl
date: 2021-07-20
author: m0wer
tags: [ 'systemd' ]
---

[timedatectl](https://www.freedesktop.org/software/systemd/man/timedatectl.html)
—- control the system time and date.

# Usage

## Get available timezones

```bash
timedatectl list-timezones
```

## Change the system timezone

```bash
timedatectl set-timezone {timezone}
```
