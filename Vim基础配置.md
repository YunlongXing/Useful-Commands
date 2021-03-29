# Vim基础配置

```$ vim ~/.vimrc```

```vim
set nocompatible
syntax on
set showmode
set showcmd
set mouse=a
set encoding=utf-8
set t_Co=256
filetype indent on

set autoindent
set tabstop=4
set shiftwidth=4
set expandtab
set softtabstop=4

set number
set relativenumber
set cursorline
set textwidth=80
set wrap
set linebreak
set wrapmargin=2
set scrolloff=5
set sidescrolloff=15
set laststatus=2
set ruler

set showmatch
set hlsearch
set incsearch
set ignorecase

set spell spelllang=en_us
set autoread
set listchars=tab:»■,trail:■
set list
set wildmenu
set wildmode=longest:list,full
```
