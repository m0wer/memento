---
title: virt-manager
date: 2021-05-02
author: m0wer
tags: [ 'virtualization' ]
---

[Virtual Machine Manager](https://virt-manager.org/) is a desktop user
interface for managing virtual machines through libvirt. It primarily targets
KVM VMs, but also manages Xen and LXC (linux containers).

# Guest additions

To enable features such as shared clipboard, drag and drop, etc. between the
host and the guest using [[virt-manager]] you need to:

1. Install
  [spice-guest-tools](https://www.spice-space.org/download/windows/spice-guest-tools/spice-guest-tools-latest.exe)
  in the [[Windows]] guest or `spice-vdagent` for a [[GNU/Linux]] one.
1. In virt-manager: Add Hardware -> Channel, set name to "com.redhat.spice.0"
  (or similar), set device type as "Spice agent (spicevmc)".

Reference: [vnc - virt-manager copy paste functionality to the vm - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/109117/virt-manager-copy-paste-functionality-to-the-vm).
