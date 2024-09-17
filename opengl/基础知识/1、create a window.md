1. init glfw：`glfwInit();`，然后才能堆窗口进行配置
2. 进行配置
	1. `glfwWindowHint();`
		1. 第一个参数是想要配置的东西
		2. 第二个参数是int，说明配置内容
3.  创建一个windows对象
	1. `GLFWwindow* window = glfwCreateWindpw(长，高，标题，NULL, NULL)`
4. 加载窗口
	1. `glfwMakeContextCurrent(window)`
5. 初始化glad
```
if(!gladLoadGLLoader((GLADloadproc)glfwGetProcAddress)){
	错误信息
}
//glfwGetProcAddress宏指向OpenGL function pointer但这个pointer和操作系统有关，这个宏返回的就是和对应操作系统有关的值
```
6. 在渲染前告诉窗口坐标和长高`glViewport(0, 0, 800, 600)`
	1. 可以设置渲染的大小小于GLFW的大小，这样就可以在窗口外渲染其他元素
	2. 第一第二的个参数的大小只能是[-1, 1]
	3. 通过回调函数来实时获取窗口的width和height`void framebuffer_size_callback(GLFWwindow* window, int width, int height){glViewport(0, 0, width, height)}`
		1. 当每次调整窗口大小就会调用这个函数，并获取长存放在width，获取高存放在height
		2. call this func：`glfwSetFrambufferSizeCallback(window, framebuffer_size_callback)`
7. 开始渲染进入render loop
```
while(!glfwWindowShouldClose(window)){
	glfwSwapBuffers(window);//双buffer机制，让没有渲染的图片显示出来
	glfwPollEvents();//这个函数用来检查有没有什么时间发生，比如键盘输入，鼠标输入。
}
```
8. 结束glfw的上下文环境，重新分配资源`glfwTerminate()`

#### 处理键盘输入
利用回调函数`glfwGetKey(window, 宏指向键盘上的键) == GLFW_PRESS`
```
void processInput(GLFWwindow* window){
	if(glfwGetKey(window, GLFW_KEY_ESCAPE) == GLFW_PRESS)
		glfwSetWindowShouldClose(window, true);
		//注意多了个Set
}
```

#### 颜色渲染
```
glClearColor(0.2f, 0.3f, 0.3f, 1.0f);
glClear(GL_COLOR_BUFFER_BIT);
```
每次调用glClear都会clear buffer 然后填充glClearColor配置的color