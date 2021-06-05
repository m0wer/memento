---
title: mmv
date: 2021-06-05
author: m0wer
tags: [ 'cli' ]
---

[`mmv`](https://github.com/itchyny/mmv) is a command line utility to
move/copy/append/link multiple files by wildcard patterns.

# Usage

The general usage scheme is:

```bash
mmv {from} {to}
```
where `{from}` is a RegEx pattern, with `*` for any substring and `?` for any
character, and `{to}` is a pattern that can include characters and
substitutions from the matching wildcards from `{from}` (using `#1` for the
first wildcard and so on).

For example (from the man page) to rename  music files from
`<track no.> - <interpreter> - <song title>.ogg` to
`<interpreter> - <track no.> - <song title>.ogg` in the current directory:

```bash
mmv '* - * - *.ogg' '#2 - #1 - #3.ogg'
```
