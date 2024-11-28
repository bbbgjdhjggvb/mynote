```cmake
cmake_minimum_required(VERSION 3.5)

project(QTAPP)

aux_source_directory(./src SRC)
add_executable(main ${SRC})

include_directories(./include)

find_package(Qt6 REQUIRED COMPONENTS Widgets Core)
target_link_libraries(main PRIVATE Qt6::Widgets Qt6::Core)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
```

### 使用.ui文件后的配置
```cmake
cmake_minimum_required(VERSION 3.5)

project(QTAPP)

find_package(Qt6 COMPONENTS Widgets Core Gui REQUIRED)

qt_standard_project_setup()

aux_source_directory(./src SRC)


qt_add_executable(main ${SRC} include/widget.h)

target_include_directories(main PRIVATE ./include ./build/include)

target_link_libraries(main PRIVATE Qt6::Widgets Qt6::Core Qt6::Gui)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

```
1. qt6使用`qt_standard_project_setup()`自动开启UI和MOC文件生成
2. 要生成MOC文件需要读取`Q_OBJECT`这个宏定义，所以在`qt_add_executable()`中添加头文件
3. 构建后会生成`ui_widget.h`和`moc_widget.cpp`