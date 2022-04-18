---
title: grep
date: 2022-04-18
author: m0wer
---

# grep

## Usage

### Common options

* `-r`: recursively search a directory.
* `-i`: ignore case.
* `-l`: print only the path of the files that have at least one match.
* `-E`: use extended RegEx.
* `-o`: print only the match.

### Limit results line length

First 400 bytes of the line:

```bash
grep "foobar" * | cut -b 1-400
```

This might leave the match out, but it's simple to use and enough for most
cases. The other option is:

```bash
grep -rEo ".{0,10}wantedText.{0,10}" *
```
