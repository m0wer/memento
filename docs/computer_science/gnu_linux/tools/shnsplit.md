---
title: shnsplit utility
date: 20180527
tags: shnsplit,FLAC,split,cue
---

# shnsplit utility

## Split multi-track FLAC to single tracks

You need the **cue** file for the times and metadata. Then: 

`shnsplit -f file.cue -t %n-%t -o flac file.flac`

[stackexchange](https://unix.stackexchange.com/questions/10251/how-do-i-split-a-flac-with-a-cue)
