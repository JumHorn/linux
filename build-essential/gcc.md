# introduction
	C language gcc
	C++ language g++

# specify header
	if there are more than one path,use multiple -I flags
```shell
gcc -I path/to/firstheaderpath -I path/to/secondheaderpath *.c
```

# generate library
1. creating static library is like normal compile process.

	Generating all obj file from the source file with *.o format.

	archieve all *.o files to generate static library that only zip them in one file.

	then use all the need to specify the path and name of the library.

2. the shared library is generated with -share and -fPIC (position independent code) command.

	gcc shared library is queit different from msvc.

	all the function in *.c files are generated with __attribute__((visibility("default"))).

	you can specify __attribute__((visibility("hidden"))) to avoid to be public visible

## create static library
	The -r flag inserts the file members into the archive.
	The -c flag creates the archive.
```shell
gcc -c path/to/*.c -o path/to/*.o
ar -rc lib*.a *.o
```

## link static library
	The -L flag indicates directory where the libraries can be found.
	The -l flag indicates the name of the library.
```shell
gcc [*.o]  -Lpath/to/staticlibrary -lstaticlibraryname -o path/to/staticlibraryname
```

## create shared library
```shell
gcc -c -fPIC path/to/*.c -o path/to/*.o
gcc -shared *.o -o *.so
```

## link shared library
```shell
gcc [*.o]  -Lpath/to/sharedlibrary -lsharedlibraryname -o path/to/sharedlibraryname
```

## standard named library vs non-standard named library
	standard named library is the format lib*.a or lib*.so and etc

1. use -lname to link a library

	it assumes the library to start with lib and end with .a (so lib and .a must not be specified)

	it actually link libname.a or libname.so

2. use **-l:name** to link a library

	non standard named library

	it will treat the name as literal rather than a name needing the "lib"

## rpath
	runtime path. to find a shared library in the executable file path for a program
	don't need to cd to the path and then execute the binary and they are relative path
	so the binary can move to anywhere as long as the relative path never changed
1. linux

	gcc link flag
```shell
-Wl,-rpath,'$ORIGIN'
```

	there should be one more $ in makefile like this -Wl,rpath,'$$ORIGIN'

2. macos

	@rpath
* for shared library
```shell
g++ -shared ./bin/transmit.o -o ./bin/libFileTransmit.so -install_name @rpath/libFileTransmit.so
```
* for executable binary
```shell
g++ main.cpp -rpath @loader_path -L ... -l ...
```

**-rpath @executable_path to find the shared library under the execute path not only the command line current working directory**

**-rpath @loader_path this does the same with the above argument**


## look up dependecies
### gcc
1. ldd to find the needed shared library
```shell
ldd libTest.so
```

2. readelf to check the executable file
```shell
readelf -d libTest.so
```

3. strings to print all printable symbols in binary
```shell
strings libTest.so
```

### clang
1. otool to check the executable file
```shell
otool libTest.so
```

# optimization
|option|optimization level|execution time|
|:---:|:---:|:---:|
|-O0|optimization for compilation time (default)|+|
|-O1 or -O|optimization for code size and execution time|-|
|-O2|optimization more for code size and execution time|--|
|-O3|optimization more for code size and execution time|---|

# others
1. embedded macro
```shell
gcc -dM -E -\</dev/null
```

2. default include path
* clang
```shell
echo | clang -v -E -x c++ -
```

* gcc
```shell
echo | gcc -E -Wp,-v -s
```

3. default search path
```shell
gcc -print-search-dirs
```

4. show compile time search path
```shell
g++ -v filename.cpp
```