# special variables

|Variable | Description|
|---------|------------|
|$0|The filename of the current script.|
|$n|These variables correspond to the arguments with which a script was invoked. Here n is a positive decimal number corresponding to the position of an argument (the first argument is $1, the second argument is $2, and so on).|
|$#|The number of arguments supplied to a script.|
|$*|All the arguments are double quoted. If a script receives two arguments, $* is equivalent to $1 $2.|
|$@|All the arguments are individually double quoted. If a script receives two arguments, $@ is equivalent to $1 $2.|
|$?|The exit status of the last command executed.|
|$$|The process number of the current shell. For shell scripts, this is the process ID under which they are executing.|
|$!|The process number of the last background command.|

# 优秀网站
> https://explainshell.com/#

# redirect(重定向Piples)
## 重定向字符串到stdin
1. one-line
```shell
cat <<< "this is coming from stdin"
```
2. delimiter
```shell
cat << EOF
line1
line2
EOF
```
3. file
```shell
cat < filename
```

## grep

很多重定向命令配合grep使用
grep -v # 反向查找不存在的字符串

## xargs

example
1. find -name *.cpp | xargs file #显示所有文件信息
2. ls -l *.cpp | xargs wc -l  #统计当前目录下所有cpp的代码行数
3. grep -IUrl $'\r' . | xargs -I{} cp {} ../ # 将所有换行符为CRLF的文件copy到上一层目录

# shell command

## regular expressions
> https://www.tutorialspoint.com/unix/unix-regular-expressions.htm

> https://www.cyberciti.biz/faq/how-to-use-sed-to-find-and-replace-text-in-files-in-linux-unix-shell/

以下软件通用的正则表达式
1. sed(stream edit)
2. ed
3. awk
4. grep
5. vi/vim

## 例子
1. sed的命令和vim的文本操作命令很像
```shell
# 在第一行行首插入abc,带i表示换行,不带i表示插入不换行
sed -i "1i s/^/abc/" input
sed -i "1 s/^/abc/" input
# 在第一行行尾插入
sed -i "1 s/$/abc/" input
# 默认只替换第一个匹配到的字符,-g全部替换
sed -i "s/abc/xyz/g" input
```

## sort
## unique
## du/df
## nc
1. tcp example
```shell
# server
nc -lvp port
# client
nc address port
```
## screen

功能和tmux重复，可以直接学习tmux

## find
### -prune

You pretty much always want the -o (logical OR) immediately after -prune, because that first part of the test (up to and including -prune) will return false for the stuff you actually want (ie: the stuff you don't want to prune out).
```shell
find [path] [conditions to prune] -prune -o \
            [your usual conditions] [actions to perform]

# example
find . -name filename -prune -o -name '*.foo' -print
find . -path pathname -prune -o -name '*.foo' -print
```
## netstat
```shell
netstat -antp
```

## unar

centos下解压rar文件
```shell
unar filename
```

## top
以下按键区分大小写

* 按内存排序

top界面按下M键(大写)
* 按CPU排序

top界面按下P键(大写)

* cpu使用率展示方式

t(小写)可再次按下切换多种样式
* 内存展示方式切换

m(小写)可再次按下切换多种样式

* 内存单位切换 e(小写)
* 保存配置 W(大写)
* 显示管理 f(小写)
* 显示帮助 h(小写)
* 显示用于排序的列 x(小写)
* 杀死进程 k(小写)
* 彩色显示 z(小写)

1. 显示单个应用程序信息
```shell
top -p PID
```