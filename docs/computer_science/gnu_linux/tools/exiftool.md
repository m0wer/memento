---
title: exiftool
date: 2017-10-17
tags: exiftool,jpg,pdf,metadata,clean,purge,privacy
---
# exiftool

## Delete metadata from a file

`exiftool -all:all= [file]`

### PDF

If it is a PDF is convnient to run this afterwards:

`qpdf --linearize [file.pdf]`

And maybe `exiftool` again.

[github](https://gist.github.com/hubgit/6078384)
