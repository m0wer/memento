---
title: rsync
date: 20171030
tags: rsync,ssh,scp,folders,copy,remote,sync
---
# rsync

## Copy folder contents and delete anything else

`rsync -avz --delete [folder] [host]:[path]`

## Exclude a path or regex

`rsync --exclude "[path/regex]"`

Where the *path* is relative to the path we want to sync.

[thegeekstuff](http://www.thegeekstuff.com/2011/01/rsync-exclude-files-and-folders/?utm_source=feedburner)
