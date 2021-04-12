---
title: Lenovo Thinkpad T14 (AMD) Gen 1
date: 2021-04-11
author: m0wer
tags: [ 't14_amd_gen1', 'thinkpad', 'lenovo' ]
---

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
