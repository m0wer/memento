---
title: Parallel
date: 2021-04-25
author: m0wer
tags: [ 'parallelization', 'gnu_linux ]
---

[GNU parallel](https://www.gnu.org/software/parallel/) is a shell tool for
executing jobs in parallel using one or more computers. A job can be a single
command or a small script that has to be run for each of the lines in the
input. The typical input is a list of files, a list of hosts, a list of users,
a list of URLs, or a list of tables. A job can also be a command that reads
from a pipe. GNU parallel can then split the input and pipe it into commands
in parallel.

For example

```bash
parallel grep "string" ::: `ls`
```
