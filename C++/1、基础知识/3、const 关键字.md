const修饰的对象内容不可修改

----
#### 一个文件中定义const变量，多个文件使用const变量
在定义和声明的时候加上extern修饰
```
//在hello.h文件中生命const变量
extern const int hello;
//在hello.cpp文件中定义const变量
extern const int hello =10;
```

----
#### const和引用
引用需要类型一致。
但是非常量，表达式，字面值，可转换类型可以赋值给const 引用

```
int i=0;
double d=21.12
const int b=0;
const int &r=b;//right
const int &r=i;//right
const int &r=32;//right
const int &r=i+32;//right
const int &r=d;//right

## 底层
const int temp =double;
const &r =temp;
```

#### const和指针
指针常量：指针指向常量
```
const int a=10;
const int *p=&a;

p=10;//false
```
常量指针：指针是常量
```
int a=10;
int b=10;
int *const p =&a;
p=b;//false
```

#### 顶层const,底层const
顶层：const修饰变量
底层：const修饰变量所指变量
### mutable
作用1：用于Debug，在const修饰的类方法中，不能使用非const修饰的成员变量，如果要使用就要用mutable进行修饰
![[Pasted image 20240810202811.png]]
![[Pasted image 20240810202831.png]]



