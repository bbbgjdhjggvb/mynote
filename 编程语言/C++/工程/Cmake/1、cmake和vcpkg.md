1. 需要让cmake知道vcpkg的位置，需要设置环境变量CMAKE_TOOLCHAIN_FILE
`set(CMAKE_TOOLCHAIN_FILE "$ENV{VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake")`
2. 运行`cmake -B build -S .`后会在build文件夹下生成.sln文件（在vs）中运行的文件。如果想要生成.exe文件需要运行命令`cmake --build build --config Release[Debug]`
3. 直接生成cmakefile文件：`需要添加参数-G "MinGw Makefiles"`，如果使用的是ninjia就`-G "ninjia"`
