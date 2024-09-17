#### std::pair类型
1. 定义：`std::pair<int,string> p=std::make_pair(1,"marry")`
2. 访问元素
	1. `p.first`
	2. `p.second`

#### std::map类型
1. 定义：`std::map<int,string> m;`
2. 插入元素：`m.insert(std::make_pair(1,"marry")`
3. 通过key访问：`m[keyvalue]`，返回value
4. 查找：`m.find(keyvalue)`，返回 __迭代器__，如果找不到返回`m.end()`
	1. 时间复杂度是`log(n)`，利用红黑树查找
5. 删除：`m.erase(keyvalue)`
6. 大小：`m.size()`
7. 遍历：for(auto &pair : m)

#### 自动排序
1. 这个容器利用红黑树实现了插入元素自动排序。
2. 默认升序
3. 自定义排序`map<int, int mycompare>`
	1. `bool operator()(const A& a0, const A &a1)const`一个const都不能少


