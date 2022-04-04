---
title: Alacritty
date: 2021-08-23
author: m0wer
tags: [ 'terminal emualtor', 'gpu' ]
---

# Alacritty

[alacritty/alacritty](https://github.com/alacritty/alacritty) is a
cross-platform, OpenGL terminal emulator.

It excels in performance, you can compare it with your previous terminal
emulator by running `time tree ~` in both.

## Install

To install it in Debian, you can use the pre-built `.deb` releases from
[barnumbirr/alacritty-debian](https://github.com/barnumbirr/alacritty-debian).

## Usage

### Shortcuts

* `Ctrl+Shift+Space`: Enter vi mode.

## Common issues

### Terminal functionality unavailable in remote shells

When connecting to a remote system from an Alacritty terminal, for instance
over SSH, it can occur that the system does not have an entry for
Alacritty in its `terminfo` database (*/usr/share/terminfo/a/alacritty*).
Therefore, all interactive terminal functionality does not work. This can be
fixed by copying the `terminfo` for Alacritty to the remote server.

On the local host, using Alacritty:

```bash
infocmp > alacritty.terminfo  # export Alacritty's Terminfo
```

Now, copy it to the remote host using `scp`.

On the remote host:

```bash
tic -x alacritty.terminfo  # import Terminfo for current user
```

*Note*: After this, you will need to start a new SSH session to have the
remote shell load the new Terminfo.

An useful`zsh` function is:

```zshrc
s () {
    infocmp | ssh $@ 'tic -x /dev/stdin'
    ssh $@
}
```

Which will setup the shell always before connecting.
