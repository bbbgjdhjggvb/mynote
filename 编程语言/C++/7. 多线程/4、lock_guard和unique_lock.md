使用mutex需要手动解锁，如果没有解锁，运行时程序会报错
### lock_guard
1. 自动加锁、解锁，原理如下
	1. 当构造函数被调用时，该互斥量会被自动锁定
	2. 当析构函数被调用时，该互斥量会被自动释放
2. `std::lock_guard`对象不能复制或移动，只能在局部作用域中使用
3. 作用域结束自动解锁。
```c++
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mtx;

void run(int &a){
    std::lock_guard<std::mutex> lock(mtx);
    for(int i = 0; i < 10000;i++){
        a += 1;
    }
}

int main(){
    int a = 1;
    std::thread t0(run, std::ref(a));
    std::thread t1(run, std::ref(a));
    t0.join();
    t1.join();

    std::cout << a <<std::endl;
    return 0;
}

```
4. 两个构造函数
	1. ![[Pasted image 20241203143005.png]]
	2. 第一个构造函数会上锁
	3. 第二个构造函数不会上锁，说明已经上锁。
		1. `std::lock_guard<std::mutex>(mtx, std::adopt_lock)`

### unique_lock
提供更多操作，基本使用和lock_guard一样
### 延时锁
1. 构造函数中传递`std::defer_lock`，表示在构造函数中不进行枷锁操作，因为下面我们要自己加上一个延时锁
2. 使用延时锁要用`std::timed_mutex`
3. `lock.try_lock_for(std::chrono::second(5))`
	1. 如果加锁成功返回true
	2. 没有成功只等待5second，返回false
```c++
#include <iostream>
#include <thread>
#include <mutex>

std::timed_mutex mtx;

void run(int &a) {
    std::unique_lock<std::timed_mutex> lock(mtx, std::defer_lock);
    if (lock.try_lock_for(std::chrono::seconds(5))) {
        for (int i = 0; i < 10000; i++) {
            a += 1;
        }
    }
}

int main() {
    int a = 1;
    std::thread t0(run, std::ref(a));
    std::thread t1(run, std::ref(a));
    t0.join();
    t1.join();

    std::cout << a << std::endl;
    return 0;
}

```