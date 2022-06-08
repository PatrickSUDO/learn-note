---
tags: 
  - vim
---

# Vim Cheatsheet

![img](https://slack-imgs.com/?c=1&o1=ro&url=https%3A%2F%2Fi.redd.it%2Fqk1hw5l34ke81.jpg)

# Vim hot key and control

- ctrl + z : put current editor to background
- fg : fetch back the current editor/Users/pai-han.su/Desktop/LightBend

### Insert mode

Go to 

- a : append
- i : insert in-place
- o: insert next line



### Commend Mode

Use `: ` to switch to 

- wq: exit and save
- q! : exit without save
- set hlsearch : search hightlight setup
---
- hjkl : equal the direction button 
- w :  move cursor forward one word (include punctuaction)
- W :  move cursor forward one word (exclude punctuaction)
- b :  move cursor backward one word (include punctuaction)
- B :  move cursor backward one word(exclude punctuaction)

- [ : forward one paragraph
-  ']' : backward one paragraph 

- gg : jump to page start
-  G: jump to page end

- $: jump to line end
-  0: jump to line start
-  ^: jump to line start not considering space or indent 

---
Search word

/[string] : search [string]
*: search string on the cursor
noh: turn off highlighting until the next search:
f[c] : search forward for next `c`
F[c] : search backward for previous`c`

n: next match string
N last match string

zz: put focus on the middle of screen
zt: put on the top of screen
zb: put on the buttom of screen

#### In Visual Mode we can select the word using cursor, hotkey like f or other ways to move cursor are also available.

v: open visual mode, select the char between cursor
V: open visual mode, select one line

y: copy 
yy: copy whole line
2yy: copy whole 2 lines

p: paste forward
P: paste backward
p[number]: paste and repeat `[number]` times 

yiw: copy the word selected by current cursor
u : undo

:set clipboard=unnamed: vim clipboard connected to out side clipboard

x: delete the char in cursor
d: delete seleted string 
D: delete string after cursor
dd: delete whole current line
dG: delete all content after cursor
dgg:  delete all content before cursor
c: delete select and go to insert mode
C: delete string after cursor and go to insert mode
\>> : add indent
\<<: reduce indent 
\=: 排版

---

:e : open file
:tabe : open a tab
gt : switch tab
gT: swith tab back

:new: open a horizontal new window on the top
:vnew: open a vertical new window on the top
ctl + w + w : switch window 

vim -o [file] [file] : open as horizontal windows
vim -O [file] [file] : open as vertical windows

---

V: visual line mode
ctrl + v : visual block mode

---

viw: select the text object of the currect char (i = inner)
v3w: select 3 text object of the currect char (i = inner)
vaw: select the text object and  the outer char of the currect char (i = inner)

vit: select the text object(with tags) of the currect char (i = inner)
vat: select the text object(with tags) and  the outer char of the currect char (i = inner)


#### v can be replaced with  d = delete, c = change, y = yank, zf = hide)

#### w can be replaced with s = sentence,  p = paragraph, t = tag 


v { : previous paragraph
v }: next paragraph

---
~:  XOR operation of upper or lower case
.: repeat last operation
J: combine multipleline into 1
ctrl + w : delete one word (insert mode)
ctrl + u: delete all words before the current cursor(insert mode)

---
:set number : display line number
:set nonumber: hide	 display line number

:! `commend` : run commend in vim

---
打开多个文件

1.vim还没有启动
  $ vim file1 file2 ... filen便可以打开所有想要打开的文件

2.vim已经启动
  :open file     再打开一个文件，并且此时vim里会显示出file文件的内容。

3.在文件之间切换焦点
  Ctrl+6—最后访问的两个文件之间切换
  :bn—下一个文件
  :bp—上一个文件


分栏显示(split)

0. 直接以分栏方式打开多个文件
 $ vim -on file1 file2 ... filen      上下分栏打开n个文件
    $ vim -On file1 file2 ... filen      左右分栏打开n个文件

1. 当前编辑文件分栏，两栏内容相同
    :sp      上下分割，快捷键Ctrl+ws
    :vsp    左右分割

2. 打开新文件新文件并与当前文件分栏
    :sp xxx  在当前文件上方栏打开文件xxx，且xxx变为当前编辑文件
    :vsp xxx  在当前文件左侧栏打开文件xxx，且xxx变为当前编辑文件

3.在各栏切换的方法
Ctrl+w+   h / j  / k /  l   ——切换到前／下／上／后栏
Ctrl+w+ ← / ↓ / ↑  / →  ——功能同上
Ctrl+ww——切换到下一个窗格中，周而复始

4. 关闭分栏
  Ctrl+w+c         松开Ctrl再按c，否则命令无效
5. 调整当前分栏大小（下面的n代表的是数字，并非字母n。省略n只缩放1行/列）
  Ctrl+w+n>      左右扩大n列
  Ctrl+w+n<      左右缩小n列
  Ctrl+w+n+      上下扩大n行
  Ctrl+w+n-      上下缩小n行



---

## vimrc

```bash
set number                                                                  
set clipboard=unnamed
set hlsearch
set cursorline
set noswapfile
```

