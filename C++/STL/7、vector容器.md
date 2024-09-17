#### 时间复杂度为O(1)的赋值操作
```
#include <algorithm>

swap(vect1, vect2);
```
1. 迭代器将失效
2. vect2不再使用

#### 初始化为10个0
```
vector<int> res(10, 0);
```