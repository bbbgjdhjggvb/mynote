是类似于hashmap的容器，查找所需的时间复杂度为`O(1)`
用法和map相似
```
unordered_map<int, int> m0, m1;
当m0和m1的key和value完全相同时，m0==m1
```

unordered_map的find成员函数根据key的哈希值进行查找，像vector\<int>没有默认hash函数编译就会报错。如果想使用需要自定义hash函数
```
class vectorhash{
	std::size_t operator()(const std::vector<int> &v)const{
		return hash;
	}
}

unordered_map<vector<int>, int, vectorhash> myHashmap;
```