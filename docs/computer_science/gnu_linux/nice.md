---
title: UNIX/Linux nice
date: 2019-06-27
tags: [ 'nice', 'niceness', 'unix', 'linux' ,'priority', 'process']
---

# UNIX/Linux nice

## Usage

### Run a process with an specific priority

```bash
nice -n [nice value] [command]
```

### Setting Priority of currently running process

```bash
renice [nice value] -p [process id]
```

## Reference

### General usage

* [thegeekdiary](https://www.thegeekdiary.com/unix-linux-how-to-change-the-niceness-priority-of-a-process/)
