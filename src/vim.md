# 打开文件
* vim flilename       打开或新建文件
* vim +n filename     打开文件，光标置于第n行
* vim + filename      open file,光标置于最后一行
* vim +/pattern filename  opne file,光标置于匹配的第一个串处
* vim -r file         打开上次编辑时崩溃的文件
* vim filename filename  打开多个文件，依次编辑

# vim配置
* set nu/number/nonumber    设置行号/取消行号
* set ruler/noruler         设置标尺/取消
* set hlsearch/nohlsearch   搜索高亮/取消
* syntax on                 语法高亮

* ignorance                 搜索忽略大小写
* number                    显示当前行号

# 光标移动
* k j l h           上下左右
* nk nj nl nh       上下左右n行
* Space             右移一个字符
* BackSpace         左移
* Enter             下移一行

* $                 当前行尾
* n$                移到第n行尾
* nG                移到第n行
* G                 移到最后一行
* gg                移到第一行

* %                 找到匹配的括号

* w/W               右移一个字至字首
* b/B               左移一个字至字首
* e/E               右移一个字至字尾

* (/)               句首/句尾
* {/}               段落首/段落尾

# 屏幕滚动
* Ctrl+u            向上滚半屏
* Ctrl+d            向下滚半屏
* Ctrl+b            向文件首滚一屏
* Ctrl+f            向文件尾滚一屏
* nz                将第几行滚动至屏幕顶部，不指定n将当前行滚动至屏幕顶部

# 插入
* i/I               光标前/当前行首
* a/A               光标后/当前行尾
* o/O               当前行之下/之上新开一行
* r/R               替换当前字符/替换当前字符及之后字符，按ESC退出
* ns/nS             删除光标向后n个字符，并进入输入模式/删除n行
* ncw/nCW           修改指定数目的字（单词）
* cc                修改一行，并输入
* nCC               修改指定数目的行

# 删除
* x/X               删除光标后/前字符
* dw                删除一个单词
* dnw               删除n个单词
* dne               删除至单词尾
* do/d$             删除至行首/尾
* dd                删整行
* ndd               删除当前行至后共n行
* dnk/j/h/l         删除上下（行,不算当前行）左右（字母）
* shift+j           删除当前行尾换行符

# 复制粘贴
* p               粘贴x或d删除的文本
* ynw             复制n个单词
* yy              复制一行
* ynl             复制n个字符
* y$              复制光标处至行尾
* nyy             复制n行

# 撤销
* u               撤销上次操作
* shift+u/U       撤销当前行所有的操作

# 搜索及替换
* /pattern        光标处向文件尾搜索
* ?pattern        光标处向文件头搜索
* n/N             同方向/反方向继续搜索
* cw newword      替换为新的word(从光标开始向后)
* .               执行替换
* :s/p1/p2/g      将当前行中p1用p2替换
* :n1,n2 s/p1/p2/g    n1行到n2行   :1,$ s/p1/p2/g(行首至行尾)
* :g/p1/s//p2/g      文件中所有的

# 行命令方式
* n1,n2 co n3   将n1至n2 拷备n3下
* n1,n2 m n3    移动
* n1,n2 d n3    删除 

# 退出
* e!        退出并重新载入
* e filename  打开filename文件
## 
* link from: https://mp.weixin.qq.com/s/PQ2tumwBrz7gwTs3KNDAPg
