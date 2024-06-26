---
title: Bash
date: 2017-10-23
author: m0wer
tags: [ 'terminal', 'console', 'run', 'bash', 'zsh', 'sh' ]
---

# Bash

## Usage

### Run a command N times

`seq [N] | xargs -Iz [command]`

[stackoverflow](https://stackoverflow.com/questions/3737740/is-there-a-better-way-to-run-a-command-n-times-in-bash)

### Output redirection

* To redirect both **stderr** and **stdout** to */dev/null* use:

```bash
command > /dev/null 2>&1
```

[stackoverflow](https://unix.stackexchange.com/questions/70963/difference-between-2-2-dev-null-dev-null-and-dev-null-21)

### For loop

```bash
for arg in [list]; do [command] $arg; done
```

### Until loop

#### Run a command until the ouptut contains some text

```bash
until somecommand | grep -q "Up to date";
do
  sleep 1;
done
```

### Environment variables

#### Remove an environment variable

To remove an exported environment variable use:

```bash
unset VARIABLE
```

#### Remove prefix/suffix

You can remove a fixed prefix and/or suffix from an environment variable
with `${var#{prefix}}` and `${var%{suffix}}` as follows

```bash
$ string="hello-world"
$
$ foo=${string#hell}
$ foo=${foo%ld}
$
$ echo "${foo}"
o-wor
```

### Arithmetic operations

Use `$(( ))`.

#### Get min or max from two variables

Use the ternary operator. For example, for `MAX(10, $VAR)` do:

```bash
$((VAR > 10 ? VAR : 10))
```

### Locks

#### flcok

To ensure only one instance of the script runs some code, you can use `flock`
as follows:

```bash
(
  # Wait for lock on /var/lock/.myscript.exclusivelock (fd 200) for 10 seconds
  flock -x -w 10 200 || exit 1

  # Do stuff

) 200>/var/lock/.myscript.exclusivelock
```

## Tips

### Beep alert

You can generate a beep alert (if enabled in the system) and a window highlight
with:

```bash
echo -e "\a"
```

## Configuration

### Prompt

#### Add timestamp

Add `\D{%T}` to `PS1` to display the current time (HH:MM:SS). For example for
debian edit */etc/bash.bashrc* and add:

```bash
PS1='\D{%T} ${debian_chroot:+($debian_chroot)}\u@\h:\w\$'
```

* [bneijt.nl](https://bneijt.nl/blog/post/add-a-timestamp-to-your-bash-prompt/)

## Reference

### Shortcuts

* [lifehacker](https://lifehacker.com/5743814/become-a-command-line-ninja-with-these-time-saving-shortcuts)

### Keyboard syntax

* [ss64](https://ss64.com/bash/syntax-keyboard.html)
