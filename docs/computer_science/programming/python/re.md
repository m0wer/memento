---
title: re
date: 2021-09-03
author: m0wer
tags: [ 'regex' ]
---

[`re`](https://docs.python.org/3/library/re.html)
provides regular expression matching operations similar to those found in Perl.

# Usage

## Split

To split a string by multiple delimiters, you can do:

```python
import re
re.split('; |, ', "string")
```
