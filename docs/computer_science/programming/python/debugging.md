---
title: Python debugging
date: 2021-04-09
author: m0wer
tags: [ 'python', 'programming'  ]
---

# pdb

 Since Python 3.7, we can just call `breakpoint()` and this will import
 [`pdb`](https://docs.python.org/3/library/pdb.html)
 (or the debugger defined in the environment variable `PYTHONBREAKPOINT`) and
 set the breakpoint in that part of the code. This will stop the program
 execution once the breakpoint is reached. Then, an interactive console while
 appear.

## Usage

The main commands are:

* `args`: Print the argument list of the current function.
* `break`: Creates a breakpoint (requires parameters) in the program execution.
* `continue`: Continues program execution.
* `help`: Provides list of commands or help for a specified command.
* `jump`: Set the next line to be executed
* `list`: Print the source code around the current line.
* `next`: Continue execution until the next line in the current function is
  reached or returns.
* `step`: Execute the current line, stopping at first possible occasion.
* `pp`: Pretty-prints the value of the expression.
* `quit`: Aborts the program.
* `return`:	Continue execution until the current function returns.

All of the above commands (except for `pp`) can be called by only its first
letter (e.g., `continue` -> `c`).
