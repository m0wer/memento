---
title: i3 window manager
date: 2017-11-02
tags: [ 'i3', 'i3wm', 'window manager', 'tiling' ]
---


# Tips

## Floating applications

`for_window [class="Nautilus" instance="file_progress"] floating enable`

* [i3wm-faq](https://faq.i3wm.org/question/61/forcing-windows-as-always-floating.1.html)

## Move workspaces between monitors

```
# move focused workspace between monitors
bindsym $mod+Ctrl+greater move workspace to output right
bindsym $mod+Ctrl+less move workspace to output left
```

* [stackoverflow](https://unix.stackexchange.com/questions/397269/i3wm-how-to-move-workspaces-between-monitors)

## How to get rid of the spinning wheel

Run `exec` and `exec_always` with `--no-startup-id` if the command won't
generate a window, otherwise the spinning wheel will get stuck and appear
instead of the normal mouse icon.
