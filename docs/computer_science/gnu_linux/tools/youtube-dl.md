---
title: youtube-dl
date: 20171113
tags: youtube-dl,download,web,audio,video,mp3,mp4
---

# youtube-dl

## Download methods

### Dowload only the audio

`youtube-dl --extract-audio [url]`

### Download audio and video in custom qualities and merge to mp4

`youtube-dl -f 'bestvideo[ext=mp4]+bestaudio[ext=m4a]/mp4' [url]`

## Tips

### Ignore errors (missing videos)

`--ignore-errors` or `-i`
