### 介绍
最大堆和最小堆：数组的最后一个元素的优先级最高（可以是最大或者是最小）
根节点的值一定大于跟节点树的所有值
插入并且堆化的时间复杂度为`log(n)`
删除并且堆化的时间复杂度为`log(n)`

#### 使用
1. 头文件：`<queue>`
2. 创建：`std::priority_queue<int>`
3. 插入元素到优先队列中：`push(value)`，自动更新优先队列
4. 移除优先队列中的优先级最高的元素：`pop()`
5. 获得优先级最高的元素：`top()`
6. 自定义优先级
	1. 默认使用的模板是`std::less<int>`，top是最大的
	2. 由于是第三个参数，所以必须包含第二个参数
```
std::priority<int,比较的容器类型vector<int>,std::greater<int>>
class mycompare{
	bool operator()(const int &a,const int &b){
		return a < b;
	}
}
```

### 遍历
```c++
while(!heap.empty()){
	cout << heap.top() <<endl;
	heap.pop();
}
```