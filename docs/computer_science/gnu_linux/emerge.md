---
title: Portage emerge (gentoo package manager)
date: 2017-10-11
tags: gentoo,portage,emerge,pacakage manager,repositories
---
# Portage emerge (gentoo package manager)

## Upgrade with depth

`emerge --ask --alert=y --update --newuse --deep 200 --with-bdeps=y --verbose @world`

## Continue failed emerge

`emerge --resume --skipfirst`
