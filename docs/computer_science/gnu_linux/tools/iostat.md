---
title: iostat
date: 2018-11-13
tags: [ 'iostat', 'linux', 'sys', 'io', 'load' ]
---

# iostat

## Usage

### Monitor all disks with extended statistics

`iostat -d -x 3 3`

* `-d`: Display the device utilization report.
* `-x`: Display extended statistics.
* `3`: Interval.
* `3`: Count.

[serverfault](https://serverfault.com/questions/871096/iostat-reports-significantly-different-util-and-await-for-two-identical-dis')
