定义一个一次性函数，在用到函数指针的地方就会可以用lambda
`[a或者是&a](int value函数的参数){函数的具体内容std::cout<<"value:"<<a<<std::endl;}`
1. a表示是值传递
2. &a表示的是引用传递
![[Pasted image 20240811220220.png]]
3. 如果想要在函数体中使用外部的变量就写在 \[  \]里
	1. 还需要添加functional头文件，并且将参数类型改为`std::functional<void(char)> out_foo`
![[Pasted image 20240811222431.png]]
4. 在一些模板函数中使用
![[Pasted image 20240811223009.png]]
