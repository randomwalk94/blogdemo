---
title: "How to exit Vim?"
date: 2019-04-08T19:22:32-04:00
categories:
- coding
tags:
- vim
- text editor
keywords:
- tech
thumbnailImage: /img/vimnail.png
---
I just want to share my `.vimrc` configuration file. Let's start with a meme

<figure>
  <img src="/img/vimmeme.png" alt="Vim meme"/>
  <figcaption><a href="https://www.reddit.com/r/ProgrammerHumor/comments/9gtq70/lady_gaga_tries_to_exit_vim/" target="_blank">Source</a>.</figcaption>
</figure>
<!--more-->

Here is the file

```vim
set nocompatible
filetype off

" enable syntax highlighting
syntax on
set t_Co=256
set background=dark
colorscheme gruvbox

set number
set tabstop=4
set expandtab
set softtabstop=4
set shiftwidth=4
set laststatus=2
set autoindent

" set whitespace in go syntax to not be colored
let g:go_highlight_trailing_whitespace_error=0

" show the matching part of the pair for [] {} and ()
" set showmatch

" configuration for gruvbox
let g:gruvbox_italic = '1'
let g:gruvbox_contrast_dark ='hard'

" quick map for nerdtree
map <C-o> :NERDTreeToggle<CR>

" quick map for copy to clipboard
command Whole execute "%w !pbcopy"
set clipboard=unnamed
vmap <C-c> "+y
vnoremap <C-c> :w !pbcopy<CR><CR>


" use mouse in Vim (yeah, why not)
set mouse=a
set ttymouse=xterm2

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')

" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'

Plugin 'lervag/vimtex'
Plugin 'itchyny/lightline.vim'
Plugin 'terryma/vim-multiple-cursors'
Plugin 'jiangmiao/auto-pairs'
Plugin 'osyo-manga/vim-over'
Plugin 'scrooloose/nerdtree'
Plugin 'morhetz/gruvbox'


" viewer for vimtex
let g:vimtex_view_method = 'skim'


" highlighting comments
let &t_ZH="\e[3m"
let &t_ZR="\e[23m"
highlight Comment cterm=italic

" autocomplete plugin for latex in vim
augroup VimCompletesMeTex
    autocmd!
    autocmd FileType tex
    \let b:vcm_omni_pattern = g:vimtex#re#neocomplete
augroup END

call vundle#end()
filetype plugin indent on
```
I use syntax highlighting plugin from [gruvbox](https://github.com/morhetz/gruvbox). It looks pretty. However, after `:PluginInstall`, I had to manually navigate to `.vim/bundle` and moved gruvbox stuff to `./vim/colors`, quite tedious indeed.  

The plugins are pretty standard. My favorite is [vim-multiple-cursors](https://github.com/terryma/vim-multiple-cursors) plugin, an (successful) attempt to replicate Sublime Text style multiple selections.  

The learning curve is quite steep, but as I feel more comfortable, I really don't to quit typing in Vim. I haven't learned enough tricks in Vim though.  

A little bit of history: Vim stands for **Vi IMproved**. It was created by [Bram Moolenaar](https://en.wikipedia.org/wiki/Bram_Moolenaar) as a clone from, you guess it, [vi](https://en.wikipedia.org/wiki/Vi) text editor of [Bill Joy](https://en.wikipedia.org/wiki/Bill_Joy).  

The philosophy behind vi is to never take your hands off the keyboard while typing. I admit the guilt of using the mouse sometimes, but that's just for convenience.  

Oh, to exit Vim, type `:q`, or `:q!`, or maybe, `:x`. 
