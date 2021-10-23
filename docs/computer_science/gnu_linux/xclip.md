---
title: xclip
date: 2019-05-02
tags: [ 'xclip', 'x11', 'x', 'clipboard' ]
---

# Usage

## Copy pipe input to clipboard

```bash
somecommand | xclip -selection clipboard
```

## Save an image from the clipboard

If you have copied an image to the clipboard and you want to save it as a file,
use:

```bash
xclip -selection clipboard -target image/png -out > out.png
```

* [stackoverflow](https://stackoverflow.com/questions/6841532/linux-image-from-clipboard)
