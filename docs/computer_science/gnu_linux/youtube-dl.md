---
title: youtube-dl
date: 2017-11-13
tags: [ 'youtube-dl', 'download', 'web', 'audio', 'video', 'mp3', 'mp4' ]
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

## Parallel downloads

```bash
youtube-dl --get-id {playlist_url} | xargs -I '{}' -P 5 youtube-dl 'https://youtube.com/watch?v={}'
```

The first command (`--get-id`) gets a list of video IDs in the playlist, one
per line. Those IDs get piped to `xargs`, which calls individual instances of
`youtube-dl` to download each video. Because we're passing `-P 5` to `xargs`,
it runs up to 5 parallel instances of `youtube-dl` at a time.

Reference: [alexwlchan](https://alexwlchan.net/2020/07/how-to-do-parallel-downloads-with-youtube-dl/)
