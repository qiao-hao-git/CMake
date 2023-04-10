# CMake

## 什么是CMake，它能干什么?

CMake的官方定义:CMake是一个开源的跨平台自动化构建系统，用来管理软件建制的程序，CMake用于使用简单的平台和编译器独立配置文件来控制软件的编译过程，并生成可在你选择的编译器环境中使用的本机makefile和工作区，CMake工具套件是由Kitware创建的，旨在响应ITK和VTK等开源项目对强大的跨平台构建环境的需求.

## CMake写的是什么?

CMakeLists.txt是我们主要写的文件,它可以帮助你的编译器链接到你所下载的外部库(Opencv, pcl等等)

在Linux系统下使用CMake生成Makefile并编译的流程如下:
1. 编写CMake配置文件CMakeLists.txt
2. 生成build文件夹
3. 进入build文件夹进行cmake ..
4. make 编译

## CMake语法

`cmake_minimum_required（VERSION 3.22)`
指定运行此配置文件所需的CMake的最低版本为3.22

`project(cmake_test)`
该命令表示项目的名称是cmake_test

`add_executable(cmake_test main.c)`
将名为main.c的源文件编译成一个名称为cmake_test的可执行文件

`aux_source_directory(. DIR_SRCS)`
查找当前目录下的所有源文件，并将名称保存为DIR_SRCS

`add_executable(cmake_test ${DIR_SRCS})`
指定生成目标

`target_link_libraries(cmake_test hello)`
添加一个名为hello的链接库

`link_directories(/A)`
添加目录使链接器能在其查找库

`target_link_directories(cmake_test include)`
将链接库目录添加到cmake_test这个target

`add_subdirectory(src)`
添加src子目录

`add_library(hello hello.c)`
生成链接库

`add_library(hello SHARED ${LIBHELLO_SRC})`
添加动态库，关键词为shared，不需要写全称libhello.so，只需要填写hello，cmake会自动生成libhello.X

`add_library(hello STATIC ${LIBHELLO_SRC})`
添加静态库，关键词为STATIC，不需要写全称libhello.a，只需要填写hello，cmake会自动生成libhello.X

`set(EXTRA_LIBS hello.c)`
将hello.c定义为EXTRA_LIBS变量

`set_target_properties(hello PROPERTIES OUTPUT_NAME "hello")`
将hello输出名称显示设置为hello,并将其设置为OUTPUT_NAME变量

`get_target_property(OUTPUT_VALUE hello OUTPUT_NAME)`
将hello名称变量设置为OUTPUT_VALUE

`MESSAGE(STATUS "This is the hello OUTPUT_NAME: " ${OUTPUT_VALUE})`
打印输出信息

`set_target_properties(hello PROPERTIES VERSION 1.2 SOVERSION 1)`
设置动态库版本号为1.2，API版本号为1

`target_link_libraries(A PUBLIC B)`
A会链接到B，当C链接A时会自动的也链接到B

`target_link_libraries(A private B)`
A会链接到B，当C链接A时若A中有B的函数，则会报错该函数未找到，此时需要增加`target_link_libraries(C PRIVATE B)`

`target_link_libraries(A INTERFACE B)`
A不会链接到B，但是C链接A的时候，A会给C提供interface，C会链接到B。

## 特殊的环境变量


## CMake官方

[CMake官方文档](https://cmake.org/cmake/help/cmake2.4docs.html)

[CMake官方主页](https://cmake.org/)

[CMake官方教程](https://cmake.org/cmake-tutorial/)

[Wiki](https://gitlab.kitware.com/cmake/community/-/wikis/Home)
