# gdb basic
	首先进入gdb调试模式，命令行下输入gdb
	file  a.exe(a.out)加载可执行程序
	r  (run)运行到断点处
	c  (continue)从断点处继续运行
	b  (Breakpoint)设置断点,可以使用“行号”“函数名称”“执行地址”等方式指定断点位置
	d  (Delete breakpoint)的简写，删除指定编号的某个断点，或删除所有断点。断点编号从1开始递增
	clear 删除断点
	s  执行一行源程序代码，如果此行代码中有函数调用，则进入该函数
	n 执行一行源程序代码，此行代码中的函数调用也一并执行
	p (Print)的简写，显示指定变量（临时变量或全局变量）的值
	显示数组p *array@len

***lldb的基本命令和上述一致***

# gdb -tui
	调试时显示源码
	refresh刷新窗口显示 快捷键Ctrl-l
	切换focus window命令 fs next

# finish

	跳出函数

# disassemble
	disassemble /m
	源码和汇编代码一起排列

# 设置参数
```shell
set args
show args
```

# 设置运行路径
```shell
set dir
show paths
```

# 显示代码内容
```shell
list # l for short
```

# 多文件断点
```shell
b filename:linenumber
b filename:functionname
```

# 查看stl的值
	查看stl值,要了解stl的实现，查看其中的成员和普通的print没什么区别
	要了解stl的实现细节，mac的stl实现和大多数的_M_imp_不一样
```gdb
(gdb) p v
$1 = {<std::__1::__vector_base<int, std::__1::allocator<int> >> = {<std::__1::__vector_base_common<true>> = {<No data fields>},
    __begin_ = 0x100300000, __end_ = 0x100300014,
    __end_cap_ = {<std::__1::__libcpp_compressed_pair_imp<int*, std::__1::allocator<int>, 2>> = {<std::__1::allocator<int>> = {<No data fields>}, __first_ = 0x100300014}, <No data fields>}}, <No data fields>}
(gdb) p v.__begin_[0]
```

	要查看iterator值的可以对地址做强制类型转化
```
(gdb) n
11          cout<<*iter<<endl;
(gdb) p iter
$3 = {__i = 0x100300000}
(gdb) p *(int *)0x100300000
$4 = 1
```
	以上过程可以一步完成,即    p=*(int*)iter
	gdb中的对象可以直接调用成员函数

# 修改内存
```shell
# 0x7fffffffeb4c 为address
set *(int*)0x7fffffffeb4c=8
```
# 修改寄存器
```
set $reg = value
```