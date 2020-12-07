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



# redirect(重定向Piples)

## grep

很多重定向命令配合grep使用
grep -v # 反向查找不存在的字符串

## xargs

example
1. find -name *.cpp | xargs file #显示所有文件信息
2. ls -l *.cpp | xargs wc -l  #统计当前目录下所有cpp的代码行数
3. grep -IUrl $'\r' . | xargs -I{} cp {} ../ # 将所有换行符为CRLF的文件copy到上一层目录

# shell command

## sed

1. sed的命令和vim的文本操作命令很像
```shell
# 在第一行插入abc,带i表示换行,不带i表示插入不换行
sed -i "1i s/^/abc/"
sed -i "1 s/^/abc/"
```
## sort
## unique
## du/df
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