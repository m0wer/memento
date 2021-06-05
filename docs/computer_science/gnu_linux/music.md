---
title: Music related stuff
date: 2018-05-21
tags: [ 'info', 'music', 'audio' ]
---

# FLAC

FLAC is a open lossless audio codec.


## ReplayGain

To calculate and add the replaygain tag to FLAC files, do:

```bash
metaflac --add-replay-gain *.flac
```

## Spot fake FLACs

To spot fake FLACs, which are FLAC files generated from a lossy audio file, you
can analyze the spectrum with `spek` or `sonic-visualiser`. Look for a cutoff
in the signal power around 16-18 kHz. If it's a real FLAC, there shouldn't such
a cut.

# Reference

## Utilities

* **easytag** for tags.
* **pulseeffects** equalizer.
* **spek** spectrum analyzer.
