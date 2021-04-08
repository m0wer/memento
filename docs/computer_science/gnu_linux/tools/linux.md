---
title: linux
date: 20171019
tags: linux,cpu,frequency,governor,scaling
---
# linux

## CPU

### Change scaling governor

`for c in $(ls -d /sys/devices/system/cpu/cpu[0-9]*); do echo ondemand >$c/cpufreq/scaling_governor; done`

[gentoo-wiki](https://wiki.gentoo.org/wiki/Power_management/Processor#Hprofile)

### Change CPU maximum frequency

`for c in $(ls -d /sys/devices/system/cpu/cpu[0-9]*); do echo [freq (Hz)] >$c/cpufreq/scaling_max_freq; done`

## Users and Groups

### Groups

You can check the groups and their members in */etc/groups*. There's also
an utility called **members**.

[cyberciti](https://www.cyberciti.biz/faq/linux-list-all-members-of-a-group/)
