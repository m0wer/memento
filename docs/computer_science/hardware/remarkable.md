---
title: reMarkable
date: 2021-06-25
author: m0wer
tags: [ 'tablet','e-ink' ]
---

reMarkable is an E-Ink writing tablet for reading documents and textbooks,
sketching and note-taking with the goal of a paper-like writing experience.

It runs GNU/Linux B-)

# Software

## reStream

Stream your reMarkable screen over SSH.

### Installation

Follow the instructions from the [repo](https://github.com/rien/reStream)

### Usage

Plug-in the reMarkable to your computer and from the computer run `restream`.

#### Options

* `-p`: portrait mode.
* `-s {ssh_destination}`: arbitrary SSH destination instead of the default
  (`root@10.11.99.1`). Useful for connecting over wifi (no need to plug it in).
