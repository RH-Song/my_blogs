---
title: CMake实践
date: 2017-02-11 22:47:19
tags: c++,CMake
categories: Programming Language
---

摘要：
文章包含对CMake简介，以及入门Demo。

<!--more-->

> 引用到的参考资料：
> 《CMake Practice》 [Gary's blog](https://durant35.github.io/2016/04/21/tool_CMake_%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/) [Hahack's blog](http://hahack.com/codes/cmake/)

## 什么是CMake
------------------------------------

如果软件想跨平台，必须要保证能够在不同平台编译。而如果使用上面的 Make 工具，就得为每一种标准写一次 Makefile ，这将是一件让人抓狂的工作。

CMake就是针对上面问题所设计的工具：它首先允许开发者编写一种平台无关的 CMakeList.txt 文件来定制整个编译流程，然后再根据目标用户的平台进一步生成所需的本地化 Makefile 和工程文件，如 Unix 的 Makefile 或 Windows 的 Visual Studio 工程。从而做到“Write once, run everywhere”。显然，CMake 是一个比上述几种 make 更高级的编译配置工具。一些使用 CMake 作为项目架构系统的知名开源项目有 VTK、ITK、KDE、OpenCV、OSG 等。

在 linux 平台下使用 CMake 生成 Makefile 并编译的流程如下：
- 编写 CMake 配置文件 CMakeLists.txt 。
- 执行命令 cmake PATH 或者 ccmake PATH 生成 Makefile。ccmake 和 cmake 的区别在于前者提供了一个交互式的界面。其中， PATH 是 CMakeLists.txt 所在的目录。
- 使用 make 命令进行编译。

一般项目工程大概如下:
```
.
├── build
| └── bin
| | └── <project_name>
├── doc
| └── <project_name>.txt
├── src
| ├── xxx.c
| └── CMakeLists.txt
├── CMakeLists.txt
├── COPYRIGHT
├── README
└── run<project_name>.sh
```

## HelloWorld工程
-----------------------------------------

在HelloWorld目录下构建工程，根据上面提到的结构树，在Helloworld目录下新建三个文件CMakeLists.txt、COPYRIGHT、README，以及三个文件夹src、doc、build。
```
mkdir HelloWorld
cd HelloWorld
touch CMakeLists.txt COPYRIGHT README
mkdir src doc build
```
此处的CMakeLists.txt内容最简单的版本可以如下：
```
# ./CMakeLists.txt
CMAKE_MINIMUM_REQUIRED(VERSION 2.8)
 
PROJECT(HELLO)
ADD_SUBDIRECTORY(src bin)
```
内容解释如下：
- “#”开头表示注释
- CMake指令大小写不敏感
- CMAKE_MINIMUM_REQUIRED(VERSION 2.8)：指定编译这个工程需要CMake的最低版本
- PROJECT(HELLO)：构建的工程的名称
- ADD_SUBDIRECTORY(source_dir [binary_dir] [EXCLUDE_FROM_ALL])：这个指令用于向当前工程添加存放源文件的子目录，并可以指定中间二进制和目标二进制存放的位置。上面的例子定义了将 src 子目录加入工程，并指定编译输出(包含编译中间结果)路径为 bin 目录。如果不进行 bin 目录的指定，那么编译结果(包括中间结果)都将存放在 build/src 目录(这个目录跟原有的 src 目录对应) 指定 bin 目录后，相当于在编译时将 src 重命名为 bin，所有的中间结果和目标二进制都将存放在 bin 目录。

在src下放源文件以及一个CMakeLists.txt,
```
cd src
touch main.cpp CMakeLists.txt
```

main.cpp内容如下：
```
#include <iostream>
using namespace std;

int main()
{
  cout << "Hello CMake." << endl;
  return 0;
}
```

src目录下的CMakeLists.txt内容如下：
```
# ./src/CMakeLists.txt
ADD_EXECUTABLE(hello main.cpp)
```
内容解析如下：
- ADD_EXECUTABLE(hello main.cpp)：这个指令用于生成目标文件，hello是工程名字，后面接着源文件，如果有多个源文件，可以用空格或者分号隔开。

这样，我们就可以开始构建了。进图build目录下，
```
cd build
cmake ..
make
```
然后可执行文件在build/bin目录下，运行hello：
```
./bin/hello
```
可以看到结果：
```
Hello CMake.
```
