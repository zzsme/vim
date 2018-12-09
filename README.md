
# A vim config

**Usage**

1. backup your vimrc file 
    
    cp ~/.vimrc ~/.vimrc_bak

2. get the config
    
    curl https://raw.githubusercontent.com/zzsme/vim/master/vimrc > ~/.vimrc

3. or use
    
    git clone https://github.com/zzs/vim.git
    ln -s vim/vimrc ~/.vimrc



```vim
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""" 
" VIM基础配置
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""" 

" 一款主题
colorscheme ron

set fenc=utf-8 
set fencs=utf-8,usc-bom,euc-jp,gb18030,gbk,gb2312,cp936 

" 不要使用vi的键盘模式，而是vim自己的 
set nocompatible 

" history文件中需要记录的行数 
set history=100 

" 在处理未保存或只读文件的时候，弹出确认 
set confirm 

" 与windows共享剪贴板 
set clipboard+=unnamed 

" 侦测文件类型 
filetype on 

" 载入文件类型插件 
filetype plugin on 

" 为特定文件类型载入相关缩进文件 
filetype indent on 

" 保存全局变量 
set viminfo+=! 

" 带有如下符号的单词不要被换行分割 
set iskeyword+=_,$,@,%,#,- 

" 语法高亮 
syntax on 

" 状态行颜色 
highlight StatusLine guifg=SlateBlue guibg=Yellow 
highlight StatusLineNC guifg=Gray guibg=White 

""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""" 
" 文件设置 
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""" 
" 不要备份文件（根据自己需要取舍） 
set nobackup 

" 不要生成swap文件，当buffer被丢弃的时候隐藏它 
setlocal noswapfile 
set bufhidden=hide 

" 字符间插入的像素行数目 
set linespace=0 

" 增强模式中的命令行自动完成操作 
set wildmenu 

" 在状态行上显示光标所在位置的行号和列号 
set ruler 
set rulerformat=%20(%2*%<%f%=\ %m%r\ %3l\ %c\ %p%%%) 

" 命令行（在状态行下）的高度，默认为1，这里是2 
set cmdheight=1 

" 使回格键（backspace）正常处理indent, eol, start等 
set backspace=2 

" 允许backspace和光标键跨越行边界 
set whichwrap+=<,>,h,l 

" 可以在buffer的任何地方使用鼠标（类似office中在工作区双击鼠标定位） 
"set mouse=a 
set selection=exclusive 
set selectmode=mouse,key 

" 启动的时候不显示那个援助索马里儿童的提示 
set shortmess=atI 

" 通过使用: commands命令，告诉我们文件的哪一行被改变过 
set report=0 

" 不让vim发出讨厌的滴滴声 
set noerrorbells 

" 在被分割的窗口间显示空白，便于阅读 
set fillchars=vert:\ ,stl:\ ,stlnc:\ 

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

" 我的状态行显示的内容（包括文件类型和解码） 
set statusline=%F%m%r%h%w\[POS=%l,%v][%p%%]\%{strftime(\"%d/%m/%y\ -\ %H:%M\")} 

" 总是显示状态行 
set laststatus=2 

""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""" 
" 文本格式和排版 
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""" 

" 自动格式化 
set formatoptions=tcrqn 

" 继承前一行的缩进方式，特别适用于多行注释 
set autoindent 

" 为C程序提供自动缩进 
set smartindent 

" 使用C样式的缩进 
set cindent 

" 制表符为4 
set tabstop=4 

" 统一缩进为4 
set softtabstop=4 
set shiftwidth=4 

" 用空格代替制表符 
set expandtab 

" 不要换行 
set nowrap 

" 在行和段开始处使用制表符 
set smarttab 

"新建.c,.h,.sh,.java文件，自动插入文件头 
autocmd BufNewFile *.cpp,*.[ch],*.sh,*.java,*.py,*.pl,*.php exec ":call SetTitle()" 
""定义函数SetTitle，自动插入文件头 
func SetTitle() 
    "如果文件类型为.sh文件 
    if &filetype == 'sh' 
        call setline(1,"\#########################################################################") 
        call append(line("."), "\# File Name: ".expand("%")) 
        call append(line(".")+1, "\# Author: ") 
        call append(line(".")+2, "\# mail: ") 
        call append(line(".")+3, "\# Created Time: ".strftime("%c")) 
        call append(line(".")+4, "\#########################################################################") 
        call append(line(".")+5, "\#!/bin/bash") 
        call append(line(".")+6, "") 
    elseif &filetype == 'python'
        call setline(1, "#!/usr/bin/env python")
        call append(line("."), "#coding=utf-8")
        call append(line(".")+1, "#File Name: ".expand("%"))
        call append(line(".")+2, "#Author: ")
        call append(line(".")+3, "#Mail: ")
        call append(line(".")+4, "#Created Time: ".strftime("%c"))
        call append(line(".")+5, "") 
    elseif &filetype == 'perl'
        call setline(1,"#!/usr/bin/env perl")
        call append(line("."), "#coding=utf-8")
        call append(line(".")+1, "#File Name: ".expand("%"))
        call append(line(".")+2, "#Author: ")
        call append(line(".")+3, "#Mail: ")
        call append(line(".")+4, "#Created Time: ".strftime("%c"))
        call append(line(".")+5, "use strict;") 
        call append(line(".")+6, "") 
        "    elseif &filetype == 'ruby'
        "        call setline(1, "#!/usr/bin/env ruby")
        "        call append(line("."), "#encoding: utf-8")
        "        call append(line(".")+1, "")
    elseif &filetype == 'php'
        call setline (1, "<?php")
        call append(line("."), "")
        call append(line(".")+1, "#File Name: ".expand("%"))
        call append(line(".")+2, "#Author: ")
        call append(line(".")+3, "#Mail: ")
        call append(line(".")+4, "#Created Time: ".strftime("%c"))
        call append(line(".")+5, "")
    else 
        call setline(1, "/*************************************************************************") 
        call append(line("."),   "  > File Name: ".expand("%")) 
        call append(line(".")+1, "  > Author: ") 
        call append(line(".")+2, "  > Mail: ") 
        call append(line(".")+3, "  > Created Time: ".strftime("%c")) 
        call append(line(".")+4, " ************************************************************************/") 
        call append(line(".")+5, "")
    endif
    if expand("%:e") == 'cpp'
        call append(line(".")+6, "#include<iostream>")
        call append(line(".")+7, "using namespace std;")
        call append(line(".")+8, "")
    endif
    if &filetype == 'c'
        call append(line(".")+6, "#include<stdio.h>")
        call append(line(".")+7, "")
    endif
    if expand("%:e") == 'h'
        call append(line(".")+6, "#ifndef _".toupper(expand("%:r"))."_H")
        call append(line(".")+7, "#define _".toupper(expand("%:r"))."_H")
        call append(line(".")+8, "#endif")
    endif
    if &filetype == 'java'
        call append(line(".")+6,"public class ".expand("%:r"))
        call append(line(".")+7,"")
    endif
    "新建文件后，自动定位到文件末尾
    autocmd BufNewFile * normal G
endfunc 


nmap <leader>w :w!<cr>
nmap <leader>f :find<cr>

nnoremap <F2> :g/^\s*$/d<CR>            " 去空行
nnoremap <C-F2> :vert diffsplit         " 比较文件

map <C-A> ggVGY                         " 映射全选+复制 ctrl+a
map! <C-A> <Esc>ggVGY
"map <F12> gg=G                          " 回到行首
vmap <C-c> "+y                          " 选中状态下 Ctrl+c 复制
map <M-F2> :tabnew<CR>                  " 新建标签
map <F3> :tabnew .<CR>                  " 列出当前目录文件
map <C-F3> \be                          " 打开树状文件目录
map <F5> :call CompileRunGcc()<CR>      " C，C++ 按F5编译运行
map <F9> :set paste<CR>                 " 进入粘贴模式，防止所粘贴内容遇到注释符号自动缩进（多么痛的领悟）
map <F10> :set nopaste<CR>              " 退出粘贴模式
map <F8> :call Rungdb()<CR>             " C,C++的调试

func! CompileRunGcc()
    exec "w"
    if &filetype == 'c'
        exec "!g++ % -o %<"
        exec "! ./%<"
    elseif &filetype == 'cpp'
        exec "!g++ % -o %<"
        exec "! ./%<"
    elseif &filetype == 'java' 
        exec "!javac %" 
        exec "!java %<"
    elseif &filetype == 'sh'
        :!./%
    elseif &filetype == 'go'
        "        exec "!go build %<"
        exec "!time go run %"       
    elseif &filetype == 'py'
        exec "!python %"
        exec "!python %<"
    elseif &filetype == 'pl'
        exec "!perl %"
        exec "!perl %<"         
    endif
endfunc

func! Rungdb()
    exec "w"
    exec "!g++ % -g -o %<"
    exec "!gdb ./%<"
endfunc

```
