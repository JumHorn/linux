# 光标移动

1. zb zz zt

	分别是将当前行移动到屏幕底(bottom) 将当前行移动到中间 和 将当前行移动到顶(top)

2. L M H

	将光标移动到当前屏幕的底端(low) 中间(middle) 和顶端(high)

3. w e b

	w光标移动到下一个单词开始,
	e光标移动到当前单词结束处,
	b光标移动到当前单词开始处

4. 查找和删除

	fa:向后查找到当前行出现a字符,
	Fa:向前查找到当前行出现a字符,
	dta:向后删除到a字符

# 光标跳转
1. 光标位置来回跳转
```shell
ctrl + o
ctrl + i
```

# 编码设置

	这里的=号左右两边不能有空格

1. 打开文件之前设置编码

```shell
vim file.txt -c "e ++enc=GB2312"
```

2. 设置文件编码

	设置打开时文件编码
```vim
:edit ++enc=utf8
```
	设置保存时文件编码
```vim
:set fileencoding=utf8
```

# 屏幕移动

1. ctrl+f ctrl+b

	向前移动一屏(forward)向后移动一屏(backward)

2. ctrl+d ctrl+u

	向后移动半屏和向前移动半屏

# 分屏显示

1. 水平分屏
```vim
:sp filepath（split）
```

2. 垂直分屏
```vim
:vsp filepath （vertical split）
```


# 键位映射

1. nnoremap - $

	inoremap is meant for insert mode mappings
	-表示跳转到行尾

# 自动补全

**YouCompleteMe**

# 更新文件

	当文件内容改变时，更新文件内容
```vim
:e
```

# 目录管理

	NERD tree
	F3打开目录管理，q退出该目录
	o打开和关闭选中的目录
	ctrl+ww在目录和打开的文件之间切换
	C以当前选中目录作为根目录
	m(menu)显示文件系统菜单(esc退出)

# 撤销与恢复

	u 撤销
	U 恢复
	ctrl+r 恢复

# 查找与替换
```vim
:%s/foo/bar/g
```
Find each occurrence of 'foo' (in all lines), and replace it with 'bar'.

```vim
:s/foo/bar/g
```
Find each occurrence of 'foo' (in the current line only), and replace it with
'bar'.

```vim
:%s/foo/bar/gc
```
Change each 'foo' to 'bar', but ask for confirmation first.

```vim
:%s/\<foo\>/bar/gc
```
Change only whole words exactly matching 'foo' to 'bar'; ask for confirmation.

```vim
:%s/foo/bar/gci
```
Change each 'foo' (case insensitive due to the i flag) to 'bar'; ask for confirmation.

# 行首和行尾插入字符
```vim
:m,n s/^/word
:m,n s/$/word
```

# 转到定义

	YouCompleteMe功能
```vim
gd(goto definition)(ycm plugin)
```

# 复制到剪切板

	其他系统下可以简单让vim使用系统剪切板
	mac自带的vim不支持剪切板
	可以先在visual 模式下选中然后再输入命令:'<,'> w !pbcopy

# 注释和反注释

	主要是在visual模式下，进行全局的添加和修改
	visual模式下选中相应的行，可以多行多列同时选择，插入时是I或者A，删除是d

# 序列生成
```vim
let i=0 | m,n g/pattern/s//\=i/ | let i=i+1
```
	从m行到n行，把pattern替换成i

# 前后复制

	4yl 从当前光标所在位置向后复制4个字符
	4yh 从当前光标所在位置向前复制4个字符
	4dl 从当前光标所在位置向后删除4个字符
	4dh 从当前光标所在位置向前删除4个字符

# 单词操作

	yw从光标处向后复制一个单词，含空格
	ye从光标处向后赋值一个单词，不含空格
	dw从光标处向后复制一个单词，含空格
	de从光标处向后赋值一个单词，不含空格

# 代码折叠

	set foldmethod=syntax
	zc关闭折叠(close)
	zo开启折叠(open)

|manual|折叠方式|
|:-:|:-:|
|indent|更多的缩进表示更高级别的折叠|
|expr|用表达式来定义折叠|
|syntax|用语法高亮来定义折叠|
|diff|对没有更改的文本进行折叠|
|marker|对文中的标志折叠|

# 正则表达式

	g/\/\//d 删除所有以双斜杠开始的注释(g表示go to line,d表示delete)

# 大小写转化

1. guw/gUw
2. gguG/ggUG
3. ggu3g

# 保存不执行格式化(no action)
```vim
:noa wq
```

# 寄存器

	vim中复制粘贴可以使用不同的寄存器，将存储历史分开管理，不像系统只用一个剪切板。
	可以通过:registers命令查看所有寄存器的的内容

1. 无名寄存器（"）：你可以直接粘贴最近一次复制或删除的文本，命令模式下使用p或者P即可。
2. 命名寄存器（a-z）：你可以通过"a到"z任意一个寄存器复制内容，比如复制一行到 a 寄存器："ayy，然后你可以在任何地方通过"ap或"aP粘贴这行内容。
3. 只读寄存器（:、.、%等）：:.p可以贴出最近一次修改的行，:%p可以贴出当前编辑的文件名等。
4. 剪贴板寄存器（+和）**：这个寄存器包含你最近一次复制到系统剪贴板的内容。你可以通过"+p或"*p粘贴剪贴板的内容。

# FAQ
## save read only file
```vim
# !sudo call sudo command
:w !sudo tee %
```