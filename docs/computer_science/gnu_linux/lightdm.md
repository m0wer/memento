---
title: lightDM
date: 2017-10-19
tags: [ 'display', 'manager', 'boot', 'session' ]
---

# lightDM

## Debug

### Fix boot fail

When booting, no X session and error in the boot log:
**/etc/X11/startDM.sh: line 22: get_options: command not found**.

**Solution**: add */lib/rc/bin/* to *ROOTPATH*:
`echo "ROOTPATH=\"/lib/rc/bin\"" >/etc/env.d/99local`

[gentoo-forum](https://forums.gentoo.org/viewtopic-p-7750666.html?sid=97faf02444a289ffe5e760e5e75bef0b)
