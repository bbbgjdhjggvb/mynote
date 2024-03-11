#### Cmake重要指令
1. cmake_minimun_required(VERSION 3.0)
2. project(Projectname[CXX][C][Java])
3. set(VAR value1 value2)：定义变量
4. include_directories(./include)
5. link_directories(./lib)
6. add_libaray(libname SHARE|STATIC ${SRC})：生成库文件
7. add_compile_options()：添加编译参数
8. add_executable(name ${RSC})：生成可执行文件
9. target_link_libraries(main libname)：为target添加需要连接的共享库
10. add_subdirectory(source_dir)：向当前工程添加存放源文件的子目录
11. aux_source_directory(. SRC)：将当前文件的所有源文件存放在SRC变量中
#### Cmake常用变量
1. CMAKE_C_FLAGS：gcc编译选项
2. CMAKE_CXX_FLAGS：g++编译选项
	1. set(CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS} -std=c++14)
3. CMAKE_BUILD_TYPE
	1. set(xxx Debug|Release)
#### 内部构建build文件夹
1. 在当前目录创建build文件夹
2. 进入到build文件夹
3. 编译上级目录中的cmakelists文件
4. 执行make生成target
#### clang
cmake DCMAKE_EXPORT_COMPILE_COMMANDS=1 ..