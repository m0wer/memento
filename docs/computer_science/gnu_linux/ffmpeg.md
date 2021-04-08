---
title: ffmpeg
date: 2019-11-04
tags: [ 'ffmpeg', 'video', 'convert' ]
---

# ffmpeg

## Usage

### List available formats
```bash
ffmpeg -formats
```

## Convert a file to the default settings

```
ffmpeg -i [input file] [output file]
```

## Compress a video to a given size

```bash
ffmpeg -i [input] -fs [size in MB]M [output]
```

* [stackexchange](https://unix.stackexchange.com/questions/28803/how-can-i-reduce-a-videos-size-with-ffmpeg)
