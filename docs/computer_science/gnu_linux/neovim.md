---
title: Neovim
date: 2022-01-07
author: m0wer
---
# Neovim

## Install

To install the latest stable release, do:

```bash
curl -sSL "https://github.com/neovim/neovim/releases/download/stable/nvim-linux64.tar.gz" | \
  tar -C "${HOME}/.local" -xz --strip-components=1 -f -
```

## Usage

### Edit remote files with SSH

Just run:

```bash
nvim scp://user@host//tmp/file
```

Notice the extra `/`. You can also specify just a directory to browse it
interactively.

## Plugins

### vim-surround

#### Shortcuts

* `ysiw"`: Surround the word under the cursor with double quotes.
* `csiw"'`: Change the quotes surrounding the word under the cursor from double
  quotes to single quotes.
* `ds'`: Delete the single quotes surrounding the word under the cursor.
* `ysi)"`: Surround the text inside parentheses with double quotes.
* `cs)]`: Change the parentheses surrounding the text inside parentheses to
  square brackets.
