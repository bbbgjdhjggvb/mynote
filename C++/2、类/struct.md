#### struct和class区别
存在唯一不切，struct默认访问权限是public,class的默认访问权限时private
#### 常量成员函数
this的默认类型时Type * const。指向调用该函数的对象。
常量成员函数
```
int add() const;//声明
int add() const{}//实现
```
常量成员函数的this的类型是const Type * const。

#### 类内声明，类外定义
```
struct xxxx{
	int add();
}
int xxxx::add(){

}
```
xxxx::作用是让编译器理解{}里面的代码是在类的作用域内
#### 构造函数初始值列表
```
struct xxx{
	int a;
	xxx(int &num1);
}
xxx::xxx(int &num1):a(num1){}
```
先执行：后面的初始化再执行括号里面的