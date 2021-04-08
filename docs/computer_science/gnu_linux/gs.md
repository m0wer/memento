---
title: ghostscript
date: 2017-10-17
tags: gs,ghostscript,pdf,compress,reduce
---
# ghostscript

## Compress PDF document

`gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/screen -dNOPAUSE -dQUIET -dBATCH -sOutputFile=output.pdf input.pdf`

"/screen" is a very poor quality. For scanned documents "/ebook" works great.

[askubuntu](https://askubuntu.com/questions/113544/how-can-i-reduce-the-file-size-of-a-scanned-pdf-file)
