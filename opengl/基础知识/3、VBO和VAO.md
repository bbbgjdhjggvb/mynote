		#### VBO
存放点的属性的数组
![[Pasted image 20240910152738.png]]
创建VBO对象
1. 创建对象`unsigned int VBO;, glGenBuffers(1, &VBO)`
1. 创建缓存`glBindBuffer(GL_ARRAY_BUFFER, VBO)`
2. 将缓存绑定数据`glBufferData(GL_ARRAY_BUFFER, sizeof(vertices)， vertices, GL_STATIC_DRAW)`
3. 告诉VAO，VBO的内存分布
```
glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 3*sizeof(float), (*void)0);
第一个参数是说明那个属性想要去配置，因为前面设置location = 0，所以写0。
第二个参数是vertex的属性个数，由于是vec3，所以是3。
第三个参数是是否开启归一化属性，由于已经归一了，所以填写GL_FALSE
第四个参数是一个顶点的大小，而不是单个属性的大小
第五个参数是offset

glEnableVertexAttribArray(0)
告诉OpenGL怎么去理解这个属性，参数是将要理解的熟悉
```

#### VAO
存放属性的数组，但是存的是指针，并且对不同属性进行归类
![[Pasted image 20240910152826.png]]
创建VAO对象
1. 创建VAO对象`unsigend int VAO;`，`glGenVertexArrays(1, &VAO)`
	1. glGxxx的第一个参数是说创建的个数
2. 绑定这个对象，上传到状态机`glBindVertexArray(VAO)`

#### 开始渲染
```
glUseProgram(shadeprogram);
//启动shader
glBindVertexArray(VAO);
//启动shader要指定是那个画布
glDrawArrays(GL_TRIANGLES, 0, 3);
//第一个说明初始面片是说明类型
//第二个参数说明要渲染的vertex的起始地址
//第三个参数说明要渲染的vertex数量
```
