---
title: GNU/Linux basics
date: 2021-12-17
author: m0wer
tags: [ 'bash', 'shell' ]
---

# GNU/Linux basics

## Useful commands

### Find duplicated lines and count how many times they appear in a file

```bash
sort <file> | uniq -c
```

### Get command output or default value if emtpy

```bash
echo | sed 's/^$/default value/'
```

### Get the cursor position

Useful for recording part of the screen with (`ffmpeg`)[ffmpeg].

```bash
watch -n 0.1 xdotool getmouselocation
```

### Generate a random string

Generate a random string to use for secrets or passwords:

```bash
head /dev/urandom | tr -dc A-Za-z0-9 | head -c10
```
