# regular makefile

	target . . . : prerequisites . . .
    	    recipe
        	. . .
        	. . .

# make
	包含一系列gcc指令的编译文件makefile
	make自动运行当前目录下的makefile文件

1. 指定makefile文件
```shell
make -f filename.mk
```

2. 多线程编译
```shell
make -f filename.mk -j 4
```

3. make install 指定安装路径
```shell
make prefix=/usr/local/ install
```

# cmake
	根据CMakeLists自动生成makefile,vs工程文件等,跨平台能力强
```shell
cmake .
```

	运行当前目录下的CMakeLists文件生成makefile文件
```shell
cmake -G
```

	查看能生茶哪些工程文件