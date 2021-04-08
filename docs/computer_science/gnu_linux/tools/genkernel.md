---
title: Genkernel
date: 2018-01-30
tags: [ 'gentoo', 'genkernel', 'kernel' ]
---

# Genkernel

## Usage

### Generate a new kernel

1. Set the desired kernel as default with `eselect`.
2. Run `genkernel all`.

#### With the kernel alias

`alias kernel='genkernel --kernel-config=/root/kernel_config all && mkkernelsig && emerge -Av @module-rebuild'`

**Note:** Steps 4 and 5 should have be done the last time, if that isn't the
case, do them first.

1. Download the new **gentoo-sources** by enabling them in package.license.
2. Select the new sources with `eselect kernel`.
3. Compile the new kernel and select new configurations with `kernel`.

After rebooting and checking that everything works as expected:

4. Save the kernel configuration with
`cp /usr/src/linux/.config ~/kernel-config-`uname -r``.
5. Copy this configurations as the default:
`cp ~/kernel-config-`uname -r` ~/kernel_config`

This will create a new clean kernel from the default configuration.

#### Preserve old configuration

Manually this will be done with `make oldconfig`.

If we save a kernel configuration, we can use it with newer versions (it will
be automatically merged with the new kernel settings). To do so, we need to
specify the old configuration to genkernel.

`genkernel --kernel-config=/root/kernel_config all`

[gentoo-forums](https://forums.gentoo.org/viewtopic-t-813106-start-0.html)
