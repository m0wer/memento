---
title: youtube-dl
date: 20171113
tags: youtube-dl,download,web,audio,video,mp3,mp4
---

# Download methods

## Dowload only the audio

`youtube-dl --extract-audio [url]`

## Download audio and video in custom qualities and merge to mp4

`youtube-dl -f 'bestvideo[ext=mp4]+bestaudio[ext=m4a]/mp4' [url]`

## Download subtitles

To download a video along with its English subtitles in `srt` format, use

```bash
youtube-dl --sub-lang en --convert-subs srt --write-sub {URL}
```

The subtitles will be written to a separate file.

# Tips

## Ignore errors (missing videos)

`--ignore-errors` or `-i`
