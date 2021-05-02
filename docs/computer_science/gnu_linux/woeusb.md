---
title: WoeUSB
date: 2021-05-02
author: m0wer
tags: [ 'windows' ]
---

[WoeUSB/WoeUSB](https://github.com/WoeUSB/WoeUSB) is a Microsoft Windows® USB
installation media preparer for GNU+Linux.

Unlike other operating systems, winbugs does not provide bootable ISOs, so a
spacial process has to be done for creating a bootable USB.

# Usage

1. Download the latest WoeUSB bash script from the releases page.
1. Download a winbugs ISO from
  [here](https://www.microsoft.com/en-in/software-download/windows10ISO).
1. Execute

  ```bash
  sudo {path to woeusb.bash} -v --target-filesystem NTFS --device {path to ISO} {path to USB device}
  ```

  Don't add the USB partition number to the device. For example use `/dev/sdb/`
  instead of `/dev/sdb1`.

  The you'll be ready to go. Fuck winbugs.
