gUU/gUgU 将当前行转换成大写
guu/gugu 将当前行转换成小写
g~~/g~g~ 将当前行进行大小写转换    
ga 显示光标下字符的ascii码
g??/g?g? 将当前行进行rot13编码
gs 默认睡眠1秒

q/ 或 q? 列出查找历史

z<CR> 把当前行移动到屏幕顶部
zt 与z<CR>类似，但光标所在列会与之前保持一致
z. 把当前行移动到屏幕中间
zz 与z.类似，但光标所在列会与之前保持一致
z- 把当前行移动到屏幕底部
zb 与z-类似，但光标所在列会与之前保持一致

CTRL-E 向下滚动一行
CTRL-Y 向上滚动一行
CTRL-F 向下滚动一屏
CTRL-B 向上滚动一屏
CTRL-D 窗口向下滚动半屏
CTRL-U 窗口向上滚动半屏

标记：
  使用字母a-z A-Z 和数字 0-9。 大写字母和数字标记是可以跨缓冲区的，而小写字母则不可以。
  特殊标记： 
           `/‘ 上一次跳转的位置
           "   最后编辑的位置
             [   最后修改的位置的开头
             ]   最后修改的位置的结尾 


寄存器：
  命名寄存器   a-z或A-Z 当使用大写字母时，内容会追加到寄存器
  编号寄存器   0-9 0包含最后yank的的内容，1包含最近delete的内容
  其他寄存器： % 包含当前文件名称(只读)
             : 包含最近执行的命令(只读)
             . 包含最后插入的文本(只读)
             # 包含当前窗口的备用文件的名称         
             " 包含最后yank或delete的内容
             _ 对该寄存器的读写什么都不会发生
             - 包含最后delete的少于一行的内容
             = 包含最后使用的正则表达式
             / 包含最后搜索的内容
             */+/~  GUI下才能使用  

快捷键：
  ～ 大小写切换
  `{marks} 跳转到标记处
  ！{motion}{filter} 执行一个外部程序filter，将motion选中的行作为filter的输入，filter执行的结果替换掉选中的行
  @{reg} 将寄存器中的内容当做VIM的指令来执行，此处的寄存器只能是0-9 a-z " . = * +
  # 向前搜索光标下的单词
  $ 移动到行的结尾
  % 跳转到对应的匹配项处(包括括号， 注释等)
  ^ 跳转到本行开头第一个非空白字符
  & 相当于 :s命令
  * 向后搜索光标下的单词
  ( 移动到上一句
  ) 移动到下一句
  0 跳转到当前行的第一个字符上
  - 移动到上[count]行的第一个非空字符上
  _ 移动到向[count -1]行的第一个非空字符上
  + 移动到下[count]行的第一个非空字符上
  ={motion} 执行equalgrp参数指定的外部程序，以{motion}选中的内容作为输入，程序执行的结果替换掉选中的内容。如果equalgrp为空，则使用函数C-indenting和lisp。


  ~ 大小写转换 @ 将寄存器的的命令当做执行 # 向前搜索光标下的单词 $ 跳转到本行末尾 % 跳转到对应的匹配项处(包括括号， 注释等) ^ 跳转到本行开关第一个非空白字符 & 相当于:s命令 * 向后搜索光标下的单词 ( 向上移动行
`a 跳转到标记a


- 光标移动到第一个非空白字符，并向上移动行 + 光标移动到第一个非空白字符，并向下移动行
_ 前面加数字，向下移动指定行，不加数字则不会移动 = 缩进(以上一行作为参考)

q reg 将接下来的输入全部记录到寄存器reg中， 再次按q停止记录 t c 向后移动到字符c的前一个位置 { 移动到上一个空行(段落) } 移动到下一个空行(段落) | 前面加数字，跳转到指定的列

u 撤消
ctrl + r 反撤消


'a 跳转到标记a所在行的行首
` 和' 都是标示上一个标记

“ 选择寄存器


- 光标移动到第一个非空白字符，并向上移动行


T c 向后移动到字符c的后一个位置


[ 后面接不同的命令，作用不一样
] 后面接不同的命令，作用不一样


; 重复上一个 f, t, F , T 命令
, 重复上一个 f, t, F , T 命令，但是方向相反
. 重复上一个使文件发生改变的命令

di( 删除当前位置括号内的内容
da( 删除当前位置括号内的内容,包括括号

ctrl + ] 跳转到光标下的主题或相关定义
ctrl + o or ctrl + t 跳到之前的位置


syntax on 会载入 &rtp下的syntax/syntax.vim
syntax on 开打语法高亮功能，并使用默认的颜色，syntax enable 打开语法高亮功能，但没有默认的颜色，可以使用highlight来设置一个自定义的颜色
filetype on 会载入&rtp下的filetype.vim文件，来通过文件名检测文件类型，如果没有检测出来，则再会载入&rtp下的scripts.vim通过文件的内容来检测文件类型
filetype plugin on 会载入 &rtp下的ftplugin.vim 来启动该功能， 然后载入&rtp/ftplugin下的相关插件(比如,C语言的插件可以是c.vim 或是c_xxx.vim，或是c文件夹下的所有.vim文件)
filetype indent on 会载入 &rtp下的indent.vim来启动该功能, 然后载入然后载入&rtp/indent.vim下的相关配置文件(C语言的配置文件是c.vim)

set laststatus = 2 "永久开打状态栏
通用格式 : %-0{minwid}.{maxwid}{item}
默认是右对齐，用 - 来设置左对齐； 0表示用0来填充空格;minwid最小宽度，maxwid是最大宽度;item可以取下列的值：
f " 文件路径
F " 完整的文件路径
y " 文件类型
l " 行号
L " 总行数
t " 文件名称

 noh： 退出高亮搜索


q 是关闭窗口
set hidden  buffer未保存时可以进行切换

tab 是窗口的集合，当tab里的最后一个窗口关闭时，tab就会被关闭

buffer是所有窗口共享的


替换命令：
     [range]s{分隔符}old{分隔符}new[{分隔符}option]
     [range]是指定行，没有range表示只对当前行进行操作。
          x 表示第x行 ，. 表示当前行，%表示所的行
          x,y 表示 x 到 y 行
          +x 表示当前行下面的第几行
          -x 表示当前行上面的第几行
          x,+y 表示从x行开始的往下y行
          x,-y 表示从x行开始的往上y行
          大部分的符号都可做分隔符
          option: 没有option ，默认只对一行中的第一个匹配进行操作
                    g  对一行的所有匹配进行操作
                    c  对操行进行确认
                    i 忽略大小写
                    p 显示出所有的替换d
          
          
安装ycm出现 YouCompleteMe unavailable no module named future
     git submodule update --init --recursive

          

slient 表示不回显命令
set hidden buffer没有保存也能切换


  let mapleader=";"
  set number
  set hidden
  set nobackup                                                                                                                                                                               
  set nowritebackup
  set cursorline
  set tabstop=4
  set shiftwidth=4
  set fillchars=vert:\ ,stl:\ ,stlnc:\ 
 set background=light
  hi vertsplit ctermbg=NONE ctermfg=0 cterm=NONE
  hi pmenu ctermbg=darkgray
  hi pmenusel ctermbg=yellow
  hi pmenusbar ctermbg=darkgray
  hi cursorline cterm=NONE ctermbg=245
  let g:asmsyntax = 'nasm'
  augroup CursorLineOnlyInActiveWindow
    autocmd!
    autocmd VimEnter,WinEnter,BufWinEnter * setlocal cursorline
    autocmd WinLeave * setlocal nocursorline
 augroup END
