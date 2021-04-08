---
title: Linux X11 Window System
date: 2018-11-02
tags: [ 'x', 'x11', 'graphic interface' ]
---

# Linux X11 Window System

## Usage

### Reload *~/.Xresources*

```bash
xrdb ~/.Xresources
```

[stackoverflow](https://stackoverflow.com/questions/21746654/reload-xresources-without-restarting-the-xterm)

## Tips

### Hide and disable the cursor

You can more or less hide it with: `unclutter -idle 0`.

To disable it, use the **Fn** button or `rmmod psmouse`.

[stackoverflow](https://stackoverflow.com/questions/660613/how-do-you-hide-the-mouse-pointer-under-linux-x11)
