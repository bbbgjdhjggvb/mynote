可以将10进制数转换为2进制，生成字符串，可以指定字符串的长度
```c++
#include <bitset>
int num = 10;
std::bitset<8> binnum(num);
```