# Notational FZF

I want to write everything in Vim. But Vim isn't optimized for
note-taking. Instead, I used
[nvALT](http://brettterpstra.com/projects/nvalt/) for years, and
whenever I had to do serious editing, I would open the file in Vim.

But some things about nvALT bugged me. It's not meant for large text
files, and opening them will cause it to lag *a lot*. I can't use
splits, and having to have a separate window open for it when I'm
working in Vim is annoying.

Plugins like [vim-pad](https://github.com/fmoralesc/vim-pad) didn't do
it for me either, because I don't want to archive my notes or use the
first line as the title since I have notes with duplicated titles. I
just want to be able to search a set of directories and create notes in
one of them, ***quickly***.

When [Junegunn](https://github.com/junegunn/) made
[`fzf.vim`](https://github.com/junegunn/fzf.vim), I realized that I
could recreate Notational Velocity in Vim.

This plugin allows you to define a list of directories that you want to
search. The first directory in the list is used as the main directory,
unless you set `g:nv_main_directory`. If you press `control-x` after
typing some words, it will use those words as the filename to create a
file in the main directory. It will then open that file in a vertical
split. If that file already exists, don't worry, it won't overwrite it.
This plugin never modifies your files at any point. It can only read,
open, and create them.

This plugin may not work on Windows. I only have a Mac to test it on. It
works for sure on Mac with Neovim, and *should* work in terminal Vim,
since it's just a wrapper over `fzf`.

## Installation

``` {.vim}
" with vim-plug
Plug 'https://github.com/Alok/notational-fzf-vim'
```

## Dependencies

`ag` is required for its fast search. I'm not planning on changing this
anytime soon.

-   [`fzf`](https://github.com/junegunn/fzf)
-   [`ag`](https://github.com/ggreer/the_silver_searcher)
-   [`fzf.vim`](https://github.com/junegunn/fzf.vim)

## Optional Dependencies

-   [`coderay`](https://github.com/rubychan/coderay), for the ability to
    preview files, with syntax highlighting.

## Required settings

You have to define a list of directories (which must be strings) to
search.

``` {.vim}
" example
let g:nv_directories = ['~/wiki', '~/writing', '~/code']
```

## Usage

This plugin unites searching and file creation. Just type in keywords
and it will search for them. It does not search in a fully fuzzy fashion
because that's less useful for prose. You can use the arrow keys or
`c-p` and `c-n` to scroll up and down the search results, and then hit
one of these keys to open up a file:

-   `c-x`: Use search string as filename and open in vertical split
-   `c-v`: Open in vertical split
-   `c-s`: Open in horizontal split
-   `c-t`: Open in new tab
-   `<Enter>`: Open highlighted search result in current buffer

The first few lines of the selected file will be visible if you have
[`coderay`](https://github.com/rubychan/coderay) installed.

## Mappings

This plugin defines a command `:NV`, and if you want a mapping for it,
then you can define it yourself. This is intentionally not done by
default. You should use whatever mapping or mappings work best for you.

For example,

``` {.vim}
nnoremap <c-s> :NV<CR>
```

## Optional settings and their defaults

``` {.vim}
" Don't forget the dot, unless you don't want one.
let g:nv_default_extension = '.md'
let g:nv_main_directory = g:nv_directories[0] " default is first in directory list
```
