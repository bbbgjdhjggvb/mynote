c++允许一次隐式类型转换
构造函数前声明、不能隐式类型转换
```
class test{
	int a;
	test(int a){
		this->a=a;
	}
}

test t=1;//将会被允许，因为等价于
test temp(1);
t=temp;

//如果加上了explicit
test t=1;//将不会被允许，因为test temp(1),t=temp将不会被允许
explicit test(int a)

可能发生错误的例子
void test (foo f){
	
}//将函数的参数限定在foo类
//如果误操作test(1)将会报错
```