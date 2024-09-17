opengl mainly work with triangle，一个矩形可以分成两个三角形进行渲染，一个球体的表面也可以分成多个三角形，这个三角形就是basic element，basic element不止三角形
#### 例如渲染一个矩形
1. 加载两个三角形的vertex
```
float vertices[] = {
	 // first triangle
     0.5f,  0.5f, 0.0f,  // top right
     0.5f, -0.5f, 0.0f,  // bottom right
    -0.5f,  0.5f, 0.0f,  // top left 
    // second triangle
     0.5f, -0.5f, 0.0f,  // bottom right
    -0.5f, -0.5f, 0.0f,  // bottom left
    -0.5f,  0.5f, 0.0f   // top left
};

可以发现有两个数据是相同的，就是左上角和右下角，可以写在一起
float vertices[] = {
	0.5f,  0.5f, 0.0f,  // top right
     0.5f, -0.5f, 0.0f,  // bottom right
    -0.5f, -0.5f, 0.0f,  // bottom left
    -0.5f,  0.5f, 0.0f   // top lef 
}
然后用另外一个数组分别表示需要用到那些元素
unsigned int indices[] = {
	0, 1, 3,
	1, 2, 3
}
```
2. 创建EBO
	1. 创建对象：`unsigned int EBO;`
	2. 生成具体对象：`glGenBuffers(1, &EBO)`
	3. 绑定状态机：`glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, EBO)`
	4. 绑定数据：`glBufferData(GL_ELEMENT_ARRAY_BUFFER, sizeof(indices), indices, GL_STATIC_DRAW)`
3. 使用
```
不是使用glDrawArrays，而是使用glDrawElements
glDrawElements(GL_TRIANGLE, 6, GL_UNSIGNED_INT, 0)
//第二个参数是需要绘制的数量，也就是indics中元素个数
//最后一个参数是offset
```
4. 渲染总程序
```
// ..:: Drawing code (in render loop) :: ..
glUseProgram(shaderProgram);
glBindVertexArray(VAO);
glDrawElements(GL_TRIANGLES, 6, GL_UNSIGNED_INT, 0);
glBindVertexArray(0);
//画数来只有就可以绑定空了
```

#### 使用流程
1. 为VAO， VBO，EBO创建空间
2. 将VAO绑定到VertexArray，一定要先，先有画布再有元素
3. 将VBO绑定到Buffer，然后绑定内容
4. 将EBO绑定到Buffer，然后绑定内容
5. 创建VertexArrayPointer
6. 开启绘制属性