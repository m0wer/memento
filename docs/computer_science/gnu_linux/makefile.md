---
title: Makefile
date: 2022-01-15
author: m0wer
---

# Configuration

## Paralelize steps

Add the following lines to the beginning of the *Makefile*:

```Makefile
NPROCS = $(shell grep -c 'processor' /proc/cpuinfo)
MAKEFLAGS += -j$(NPROCS)
```
