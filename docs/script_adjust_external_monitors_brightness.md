---
title: Script to adjust external monitor brightness
date: 2022-04-02
author: m0wer
---

# Script to adjust external monitor brightness

If you want to adjust the external monitor brightness according to the main
display, you can run the following script after every brightness change to the
main monitor.

```bash
#!/usr/bin/env bash

# check if external monitor connected
xrandr -q | grep -q "DisplayPort-4 connected" || exit 0

(
  # Wait for lock on /var/lock/adjust_external_monitors_brightness.exclusivelock (fd 200) for 20 seconds
  flock -x -w 20 200 || exit 1

  # main screen brightness (from 0 to 255)
  main=$(cat /sys/class/backlight/amdgpu_bl0/brightness)

  # external monitor
  l27_max=100 # max brightness
  l27_0=40 # equivalent brightness of main for l27 min brightness
  l27_100=255 # equivalent brightness of main for l27 max brightness

  # equivalent brightness for the external monitor
  l27=$(( 100 * ( (main > l27_0 ? main : l27_0) - l27_0 ) / (l27_100 - l27_0) ))

  # try to set it until success
  until ddccontrol -r 0x10 -w $l27 dev:/dev/i2c-11 | grep -q "Writing 0x10";
  do
    sleep 1;
  done

) 200>/var/lock/adjust_external_monitors_brightness.exclusivelock
```

You will need to make a few adjustments:

* Change `DisplayPort-4` to whatever corresponds to your external monitor.
* Change `/sys/class/backlight/amdgpu_bl0/brightness` if you use Intel.
* Adjust the variables (`l27_max`, `l27_0`, `l27_100`).
* Get the corresponding i2c device (change `i2c-11`) by running `ddccontrol -p`.
