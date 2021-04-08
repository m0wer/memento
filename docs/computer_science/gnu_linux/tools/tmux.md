---
title: tmux
date: 2017-10-29
tags: [ 'tmux', 'ssh', 'shell' ]
---

# tmux

## Usage

### Managing panes and windows

#### Resize a pane

**Ctrl+b** and then:

```
:resize-pane -D (Resizes the current pane down)
:resize-pane -U (Resizes the current pane upward)
:resize-pane -L (Resizes the current pane left)
:resize-pane -R (Resizes the current pane right)
:resize-pane -D 10 (Resizes the current pane down by 10 cells)
:resize-pane -U 10 (Resizes the current pane upward by 10 cells)
:resize-pane -L 10 (Resizes the current pane left by 10 cells)
:resize-pane -R 10 (Resizes the current pane right by 10 cells)
```

[micahelsoolee](https://michaelsoolee.com/resize-tmux-panes/)

## Config

### Default setup

Create a file with the instructions. For example *~/.tmux/main*:

```
#main
new  -s main htop
splitw -v -p 50 -t 0 "docker stats $(docker ps --format '{{.Names}}')"
splitw -h -p 50 -t 0 nload eth0
neww
selectw -t 0
selectp -t 2
```

And then source it with a bind or by default (so it is used when running `tmux
a` without an existing session) in *~/.tmux.conf*:

```
source-file ~/.tmux/main
```

[stackoverflow](https://stackoverflow.com/questions/5609192/how-to-set-up-tmux-so-that-it-starts-up-with-specified-windows-opened)

## Debug

### Protocol version mismatch

When upgrading a system and trying to attach an existing Tmux session that was
created with a different version of the currently installed one.

```bash
pgrep tmux
/proc/[pid]/exe attach
```

* [stackexchange](https://unix.stackexchange.com/questions/122238/protocol-version-mismatch-client-8-server-6-when-trying-to-upgrade)
