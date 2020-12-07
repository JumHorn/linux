# introduction
C language gcc
C++ language g++
it is neccessary to specify the current directory with -L . to find the library

# specify header
> gcc -I path/to/firstheaderpath *.c

if there are more than one path,use multiple -I flags

# generate library
creating static library is like normal compile process.Generating all obj file from the source file with *.o format.archieve all *.o files to generate static library that only zip them in one file.then use all the need to specify the path and name of the library.

the shared library is generated with -share and -fPIC (position independent code) command.

gcc shared library is queit different from msvc. all the function in *.c files are generated with __attribute__((visibility("default"))).you can specify __attribute__((visibility("hidden"))) to avoid to be public visible

## create static library
> gcc -c   path/to/*.c    -o path/to/*.o \
> ar -rc lib*.a *.o

The -r flag inserts the file members into the archive.
The -c flag creates the archive.

## link static library
> gcc [*.o]  -Lpath/to/staticlibrary -lstaticlibraryname -o path/to/staticlibraryname

The -L flag indicates directory where the libraries can be found.
The -l flag indicates the name of the library. Note, that it assumes the library to start with lib and end with .a (so lib and .a must not be specified)

## create shared library
> gcc -c -fPIC  path/to/*.c    -o path/to/*.o \
> gcc -shared *.o -o *.so

ln -s *.so path/to/*.so
this statement above can be omitted

## link shared library
> gcc [*.o]  -Lpath/to/sharedlibrary -lsharedlibraryname -o path/to/sharedlibraryname

## rpath
runtime path. to find a shared library in the executable file path for a program. \
don't need to cd to the path and then execute the binary and they are relative path \
so the binary can move to anywhere as long as the relative path never changed. \
1. linux \
gcc link flag
> -Wl,-rpath,'$ORIGIN'

there should be one more $ in makefile like this -Wl,rpath,'$$ORIGIN'

2. macos \
@rpath
* for shared library
g++ -shared ./bin/transmit.o -o ./bin/libFileTransmit.so -install_name @rpath/libFileTransmit.so \
* for executable binary \
g++ main.cpp -rpath @loader_path -L ... -l ...

**-rpath @executable_path to find the shared library under the execute path not only the command line current working directory**

**-rpath @loader_path this does the same with the above argument**


## look up dependecies
### gcc
1. ldd to find the needed shared library
> ldd libTest.so

2. readelf to check the executable file
> readelf -d libTest.so

3. strings to print all printable symbols in binary
> strings libTest.so

### clang
1. otool to check the executable file
> otool libTest.so

# conclusion
when code compiling,the sharedlibrary name must be lib*.so the -l parameter depend on the name.
when run the program,let the lib*.so stay under the same directory with the execute file and the name of the library must be *.so.
another way to solve this problem is to add evironment variable whitch I don't like at all

# optimization
|option|optimization level|execution time|
|:---:|:---:|:---:|
|-O0|optimization for compilation time (default)|+|
|-O1 or -O|optimization for code size and execution time|-|
|-O2|optimization more for code size and execution time|--|
|-O3|optimization more for code size and execution time|---|

# others
1. embedded macro
> gcc -dM -E -\</dev/null

2. default include path
* clang
> echo | clang -v -E -x c++ -

* gcc
> echo | gcc -E -Wp,-v -s