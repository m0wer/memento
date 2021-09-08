---
title: ImageMagick
date: 20171029
tags: imagemagick,screenshot
---

# Screenshots

## Make a screenshot of a selection

`import [output.png]`

[stackexchange-unix](https://unix.stackexchange.com/questions/233345/how-can-i-easily-make-screenshots-of-screen-regions-on-arch-linux-with-i3-wm)

# Conversions

## Image to PDF

`convert [image] [output].pdf`

[stackoverflow](https://stackoverflow.com/questions/8955425/how-can-i-convert-a-series-of-images-to-a-pdf-from-the-command-line-on-linux)

## Resize and compress

Resize an image to width 1000 px and compress it with a JPG quality level of
80% in place:

```bash
mogrify -quality 1000 -resize 80 file.jpg
```
