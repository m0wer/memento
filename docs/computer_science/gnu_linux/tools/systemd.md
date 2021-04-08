---
title: systemd
date: 2017-10-26
tags: [ 'systemd', 'unit', 'services', 'configuration' ]
---

# systemd

## Usage

### Changing directory

In a *unit.service* file:

```systemd
[service]
WorkingDirectory=[path]
```

[unix-stackexchange](https://unix.stackexchange.com/questions/200654/executing-chdir-before-starting-systemd-service)

### Setting a start timeout

`TimoutStartSec=`

### Setting a dealy before restarting

`RestartSec=`

## Debug

## Service unit dependency error

Instead of using **Requires=** try using **Wants=** so that **systemd** won't
fail and retries if configured to do so.
