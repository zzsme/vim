### 前提

Git curl

### 第一步

设置 Vundle, the plug-in manager for Vim 
```
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

### 第二步

编辑配置文件
`vim .vimrc`

设置粘贴模式
`:set paste`

粘贴以下内容
```
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
"基础配置
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
set nocompatible

" 主题
"colorscheme molokai
"colorscheme desert
colorscheme ron

" 基础设置
"set guifont=Monaco:h12          " 字体 && 字号
"set guifont=Consolas\ for\ Powerline\ FixedD:h12
syntax on                       " 打开语法高亮
"set number                      " 显示行号
"set relativenumber              " 显示光标所在的当前行的行号，其他行都为相对于该行的相对行号。
set autoindent                  " 设置缩进有三个取值 cindent (c风格)
                                " smartindent (智能模式)、
                                " autoindent (简单的与上一行保持一致)
set tabstop=4                   " 设置 tab 键的宽度
set shiftwidth=4                " 换行时行间交错使用4个空格
set backspace=indent,eol,start  " 设置退格键可用
                                " indent：如果用了 set indent, set ai 等自动缩进，想用退格键将字段缩进的删掉，必须设置这个选项，否则不响应。
                                " eol：如果插入模式下在行开头，想通过退格键合并两行，需要设置eol。
                                " start：要想删除此次插入前的输入，需设置这个。
set expandtab                   " 由于 Tab 键在不同的编辑器缩进不一致，该设置自动将 Tab 转为空格
set softtabstop=4               " Tab 转为多少个空格
set smarttab                    " 每次按 backspace 时删除4个空格
set incsearch                   " 增量式搜索(遍搜索遍显示内容)
set hlsearch                    " 高亮搜索
filetype on                     " 打开文件类型检测功能
filetype plugin on              " 允许加载文件类型插件
filetype indent on              " 允许为不同类型的文件定义不同的缩进格式
set showmatch                   " 显示括号配对情况
"set foldenable                 " 开启代码折叠
"set foldmethod=syntax          " 自动语法折叠
set nobackup                    " 禁止生成备份
set noswapfile                  " 不产生 swp 文件
set mouse=a                     " 启用鼠标
set nowrap                      " 设置不自动折行
"set cursorline                  " 突出显示当前行
set clipboard=unnamed           " 与 windows 共享剪贴板
set cmdheight=1                 " 命令行（在状态行下）的高度，默认为1
set laststatus=2                " 是否显示状态栏。0 表示不显示，1 表示只在多窗口时显示，2 表示显示

set history=1000


"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
" 搜索和匹配
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

" 高亮显示匹配的括号
set showmatch

" 匹配括号高亮的时间（单位是十分之一秒）
set matchtime=5

" 在搜索的时候忽略大小写
set ignorecase

" 不要高亮被搜索的句子（phrases）
set nohlsearch

" 在搜索时，输入的词句的逐字符高亮（类似firefox的搜索）
set incsearch

" 输入:set list命令是应该显示些啥？
set listchars=tab:\|\ ,trail:.,extends:>,precedes:<,eol:$

" 光标移动到buffer的顶部和底部时保持3行距离
set scrolloff=3

" 不要闪烁
set novisualbell

" 设置窗口
if has("gui_running")
    " au GUIEnter * simalt ~x   " 窗口启动时自动最大化
    winpos 70 25                " 指定窗口出现的位置，坐标原点在屏幕左上角
    set lines=55 columns=180    " 指定窗口大小，lines 为高度，columns 为宽度
    set guioptions+=c           " 使用字符提示框
    set guioptions-=m           " 隐藏菜单栏
    set guioptions-=T           " 隐藏工具栏
    set guioptions=L            " 隐藏左侧滚动条
    set guioptions=r            " 隐藏右侧滚动条
    set guioptions-=b           " 隐藏底部滚动条
    set showtabline=0           " 隐藏 Tab 栏
endif

" 设置编码
set fenc=utf-8                              " 设置编码
set encoding=utf-8                          " 内部的程序识别编码
set fileencoding=utf-8                      " 当前文件编辑时使用的文件编码
set fileencodings=utf-8,gbk,cp936,latin-1   " gvim 打开文件是支持的编码
set ambiwidth=double                        " 防止特殊符号无法显示
set helplang=cn                             " 中文帮助

if has("win_32")
    " 解决菜单乱码
    "source $VIMRUNTIME/delmenu.vim
    "source $VIMRUNTIME/menu.vim
    " 解决consle输出乱码
    "language messages zh_CN.utf-8
endif


" 以下为插件管理
set laststatus=2  "永远显示状态栏
set t_Co=256      "在windows中用xshell连接打开vim可以显示色彩

set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()

Plugin 'VundleVim/Vundle.vim'
Plugin 'vim-airline/vim-airline'
Plugin 'vim-airline/vim-airline-themes'

Plugin 'scrooloose/nerdtree'
Plugin 'majutsushi/tagbar'
Plugin 'kien/ctrlp.vim'
call vundle#end()

"let g:airline_theme="luna"
let g:airline_theme='bubblegum'

"这个是安装字体后 必须设置此项
let g:airline_powerline_fonts = 1

"打开tabline功能,方便查看Buffer和切换，这个功能比较不错"
"我还省去了minibufexpl插件，因为我习惯在1个Tab下用多个buffer"
let g:airline#extensions#tabline#enabled = 1
"let g:airline#extensions#tabline#buffer_nr_show = 1

"设置切换Buffer快捷键"
nnoremap <C-N> :bn<CR>
nnoremap <C-P> :bp<CR>

" 关闭状态显示空白符号计数,这个对我用处不大"
let g:airline#extensions#whitespace#enabled = 1
let g:airline#extensions#whitespace#symbol = '!'

" 在Gvim中我设置了英文用Hermit， 中文使用 YaHei Mono "
if has('win32')
  set guifont=Hermit:h13
  set guifontwide=Microsoft_YaHei_Mono:h12
endif

```


启动vim 执行 `:PluginInstall`

或者命令行执行
To install from command line: `vim +PluginInstall +qall`
