`#include <variant>`
当一个变量要有多个类型时可以使用这个
`std::varient<std::string,int> data`说明data变量有string类型和int类型，但不可能既是string又是int
`data="hello`，就说明了这个变量是string类型，用`std::get<std::string>(data)`来获取变量
如果`data=10`，用`std::get<std::string>(data)`就会抛出异常，不会在编译器报错
