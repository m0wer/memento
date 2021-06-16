---
title: pdftk
date: 2020-01-28
tags: [ 'pdftk', 'pdf' ]
---

# Usage

## Rotate all of the pages clockwise

```bash
pdftk [input] cat 1-endeast output [output]
```

## Extract a page range of a PDF

To extract a page range of a PDF you could print to file using `evince`
selecting a page range. The drawback of this method is that the text might be
converted to images an thus no longer be searchable. A faster alternative that
also keeps the text intact is using `pdftk` as follows:

```bash
pdftk {original.pdf} cat {range_start}-{range_end} output {output.pdf}
```

where `{range_start}` is the first page number of `{original.pdf}` to be
included in `{output.pdf}` and `{range_end}` the last one.

# Reference

## Docker images

* [jottr/alpine-pdftk](https://github.com/jottr/alpine-pdftk)
