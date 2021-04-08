---
title: vim
date: 2017-10-29
tags: [ 'vim', 'text editor', 'cli' ]
---

# vim

## Usage

### Windows (split mode)

#### Switch between windows

**Ctrl+w** and the direction. Useful for `vimdiff`.

[quora](https://www.quora.com/How-do-I-switch-between-panes-in-split-mode-in-Vim)

### Links

#### Follow link

**Ctrl+]**

[wikia](http://vim.wikia.com/wiki/Learn_to_use_help)

### Spell checking

1. To move to a misspelled word, use **]s** and **[s**.
2. To show suggestions use **z=**.
3. To add a word to the dictionary use **zg**.

To mark a correct word as misspelled, use **zw**.

[linux](https://www.linux.com/learn/using-spell-checking-vim)

### Set tabulation

Execute `set tabstop=2 shiftwidth=2 expandtab` and then, it's a good idea to
execute `:retab`.

[stackoverflow](https://stackoverflow.com/questions/426963/replace-tab-with-spaces-in-vim)

### Registers

Vim saves the "clipboard" history as registers. You can check the saved ones
with `:reg`.

If you want to paste the content of one of them use `"3p` for example.

**Reference**:
[superuser](https://superuser.com/questions/102815/vim-cut-and-paste-history#102828)

## Tips

### Go to th nth line

`[n]G` for example: `42G`.

[wikia](http://vim.wikia.com/wiki/Go_to_line)

### Set filetype (useful for snippets)

`:set filetype=[filetype]`

### Disabling line numbers

Useful for copying.

`:set norelativenumber`

[wikia](http://vim.wikia.com/wiki/Display_line_numbers)

### Deleting trailing whitespaces automatically

Add the following line to your *.vimrc* to automatically delete the trailing
whitespaces when saving the file if it's one of the specific file types:

`autocmd FileType c,cpp,java,php autocmd BufWritePre <buffer> %s/\s\+$//e`

[wikia](http://vim.wikia.com/wiki/Remove_unwanted_spaces#Automatically_removing_all_trailing_whitespace)

### Breaking long lines automatically

`set textwidth=79`

[stackexchange](https://vi.stackexchange.com/questions/574/keeping-lines-to-less-than-80-characters)

### Change filetype based on directory path

`autocmd BufRead,BufNewFile [path regex] set syntax=html`

[wikia](http://vim.wikia.com/wiki/Change_filetype_based_on_directory_path)

### Autoindent with tab as 4 spaces

Set in .vimrc the following lines:

```vimrc
syntax enable
set smartindent
set tabstop=4
set shiftwidth=4
set expandtab
```

If you are working on a file and you want to indent it automatically from the
beginning to the end use `gg=G`.

* [coderwall](https://coderwall.com/p/vyckiw/vim-auto-indent-4-spaces)

## Plugins

### Syntastic

#### Disable Syntastic

`:SyntasticToggleMode`

[stackoverflow](https://stackoverflow.com/questions/20030603/vim-syntastic-how-to-disable-the-checker)

## Debug

### Plugins

#### CtrlP

##### CtrlP changes working directory annoyingly

Disable working path mode feature: `let g:ctrlp_working_path_mode = '0'`

[stackoverflow](https://stackoverflow.com/questions/11873736/vim-ctrlp-plugin-manually-set-root-search-directory)

#### UltiSnips and YouCompleteMe

Since by default they both use **<Tab>** as a expand tab, we must do something
about it. Using the SuperTab plugin:

```vimrc
" make YCM compatible with UltiSnips (using supertab)
let g:ycm_key_list_select_completion = ['<C-n>', '<Down>']
let g:ycm_key_list_previous_completion = ['<C-p>', '<Up>']
let g:SuperTabDefaultCompletionType = '<C-n>'

" better key bindings for UltiSnipsExpandTrigger
let g:UltiSnipsExpandTrigger = "<tab>"
let g:UltiSnipsJumpForwardTrigger = "<tab>"
let g:UltiSnipsJumpBackwardTrigger = "<s-tab>"
````

* [stackoverflow](https://stackoverflow.com/questions/14896327/ultisnips-and-youcompleteme)

## Reference

* [spell checking](https://www.linux.com/learn/using-spell-checking-vim)
* [window movement](https://www.cs.oberlin.edu/~kuperman/help/vim/windows.html)

### Registers

* [stackoverflow](https://stackoverflow.com/questions/1497958/how-do-i-use-vim-registers)
* [brianstorti](https://www.brianstorti.com/vim-registers/)

### Plugins

* [vim-autoclose](https://github.com/Townk/vim-autoclose): enable an auto-close
  chars feature.
