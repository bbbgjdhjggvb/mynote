 包含头文件chrono
1. 获得当前时间`std::chrono::high_resolition_clock::time()`
	1. 会返回当前时间对象，类型很长
2. 计算时间差`std::chrono::duration<float> duration=end-start`
	1. `std::cout<<durarion.count()<<std::endl`
![[Pasted image 20240812121637.png]]
