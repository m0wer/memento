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

### Shortcuts

* Open the previous buffer: `<C-^>` (or `<C-6>` in some keyboards).

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

### vim-fugitive

[tpope/vim-fugitive: fugitive.vim: A Git wrapper so awesome, it should be illegal](https://github.com/tpope/vim-fugitive)

#### Cherry pick lines

1. Open the git summary with :Git (or :G).
1. Expand the file which contains the lines you want to stage with `>`
  (or `=` to toggle). This will only show the changed chunks plus some extra
  lines of context above and below the changed lines.
1. `V` to start visual mode and select the lines you want to stage with `hjkl`.
1. `s` to stage the visual selection (or `-` to toggle)
1. Repeat 2-4 as needed
1. `cc` to commit

## Mappings

### Search for visual selection

```vimrc
vnoremap // y/\V<C-R>=escape(@",'/\')<CR><CR>
```
To use the mapping, visually select the characters that are wanted in the
search, then type `//` to search for the next occurrence of the selected text.

## Marks

A mark allows you to record your current position so you can return to it
later.

Usage:

* `:marks`: show existing marks.
* `ma`: set mark `a` in current position of current file, accessible only from
  the current file.
* `mA`: set mark `A` in current position of current file, accessible from
  anywhere.
* `'a`: Go to mark `a`.
* `]'`: jump to next line with a lowercase mark.

## sed

### Replace with newline

When replacing some match with a newline, if you try to put `\n` you will see
that a null character is inserted. You should use `\r` (carriage return)
instead of `\n`.

### Without RegEx

Use `:sno` instead of `:s` to disable magic.
