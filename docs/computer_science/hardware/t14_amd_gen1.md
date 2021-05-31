---
title: Lenovo Thinkpad T14 (AMD) Gen 1
date: 2021-04-11
author: m0wer
tags: [ 't14_amd_gen1', 'thinkpad', 'lenovo' ]
---

# Usage

## BIOS upgrade

There are several ways of upgrading the BIOS of this laptop. One of them is
using `fwupdate`, other is running an executable from winbugs and the last one
is from a bootable USB.

Keep in mind that the upgrades might require the laptop to be plugged to a power
supply and/or have a level of charge over 50%, 80%...

### Bootable USB

First, create the bootable USB:

1. Download the BIOS update (Bootable CD) from
  [lenovo](https://pcsupport.lenovo.com/es/en/products/laptops-and-netbooks/thinkpad-t-series-laptops/thinkpad-t14-type-20ud-20ue/downloads/driver-list/component?name=BIOS%2FUEFI).
1. Check the integrity of the downloaded file with `sha256sum {downloaded_file}`
1. Extract the bootable image:
  ```bash
  geteltorito -o t14.img {downloaded_file}
  ```
1. Flash the extracted image to an usb:
  ```bash
  dd if=t14.img of=/dev/sdX
  ```
1. Reboot, interrupt the boot (press enter), press F12 and select the USB as
  the boot device.
1. Follow the on-screen instructions.

# Issues

## Flashing colors on the LCD screen

!!! note "TL;DR: power off the laptop and unplug it from the AC adapter and press the emergency-reset button located in the bottom case."

I opened my laptop, which was suspended, and the screen was flashing in
different colors as shown on this video

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/HWugyoWqjqA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

I panicked a bit and look the problem up, finding only [this thread](https://forums.lenovo.com/t5/ThinkPad-T400-T500-and-newer-T-series-Laptops/Thinkpad-T14-gen-1-AMD-LCD-change-colors-green-blue-red-etc/m-p/5060359)
where they suggested reinstalling the BIOS by using an external screen. I've
tried to do so by connecting the laptop to the [ThinkPad USB-C Dock Gen 2](https://www.lenovo.com/us/en/accessories-and-monitors/docking/universal-cable-docks-usb/TP-USB-C-DOCK-GEN2-US/p/40AS0090US)
but the screens showed no output.

Before trying anything else, I decided to go for the ol' reliable "have you
tried turning it off and on again". So I opened the bottom case, which is a bit
annoying  but easily doable, as shown on the following video

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/AeO9oklP7sg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Then, I unplugged the battery and the BIOS button battery and replugged them again.
I checked that it worked properly before putting back the bottom case.

But then, I've learned that Thinkpads with a non-removable battery generally
have a "emergency-reset hole", which I could have just pressed instead of
opening the laptop xD There is more information about it in the [T14 Gen 1 and P14s Gen 1 Hardware Maintenance Manual](https://download.lenovo.com/pccbbs/mobiles_pdf/t14_gen1_p14s_gen1_hmm_en.pdf).
