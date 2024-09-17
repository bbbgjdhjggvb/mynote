项目主文件下的CMakeLists.txt
```
enable_testing()启动测试

add_subdirectory(./test/)
```

test/文件下的CMakeLists.txt
```
add_executable()

target_link_libraries(test可执行文件 gtest_main gtest)

add_test(
	NAME 随便起的区分各个测试的名字
	COMMAND test
)
add_test()
```

#### Test Command
```
cd build/
ctest
```