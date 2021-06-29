---
title: ffmpeg
date: 2019-11-04
author: m0wer
tags: [ 'ffmpeg', 'video', 'convert' ]
---

# Usage

## Recording

### Record video from screen and audio from microphone

```bash
ffmpeg -video_size 1920x1080 -framerate 30 -f x11grab -i :0.0+0,0 -f alsa -ac 2 -i pulse -pix_fmt yuv420p {out}
```

With `-i :0.0+0,0` you can specify the X11 session (`0.0`) and the position of
the top left corner (`0,0`).

## Misc

### List available formats
```bash
ffmpeg -formats
```

### Convert a file to the default settings

```
ffmpeg -i [input file] [output file]
```

### Compress a video to a given size

```bash
ffmpeg -i [input] -fs [size in MB]M [output]
```

* [stackexchange](https://unix.stackexchange.com/questions/28803/how-can-i-reduce-a-videos-size-with-ffmpeg)

# Tips

## Video compatibility

For compatibility with common media players, use `-pix_fmt yuv420p` and `MP4`
format.
