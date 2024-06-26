---
title: neomutt
date: 2018-11-18
author: m0wer
tags: [ 'email', 'mutt', 'neomutt', 'imap', 'smtp', 'pop', 'vim', 'solarized' ]
---

# NeoMutt

## Usage

### GPG

#### Attach GPG public key

When sending an email you might want to attach your GPG public key. Press
**Alt+k** in order to do so.

* [myridia.com](https://myridia.com/dev_posts/view/236)

## Delete/Undelete

### All

To delete or undelete all:

1. Press `D` or `U`.
1. Enter `~A` to mark all.

## Mailboxes

Commands:

* `c?<Tab>`: (on top of a mailbox) Shows all subdirectories and allows to open
  them.

## Configuration

### index_format

This variable allows you to customize the message index display to your
personal taste.

#### Local timezone

Use `%{fmt}` for the sender's timezone and `%[fmt]` for your local one.

## Reference

* [arch-wiki](https://wiki.archlinux.org/index.php/mutt)

### Vim bindings

* [ryanlue](https://ryanlue.com/posts/2017-05-21-mutt-the-vim-way)
