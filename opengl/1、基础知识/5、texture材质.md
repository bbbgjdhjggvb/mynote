### texture coodinate
材质是一张图片，我们要设置模型上各个点在材质图片的那个位置。例如下面的图片：
![[Pasted image 20240925161533.png]]
```c++
float texCoords[] = {
	0.0f, 0.0f,  // lower-left corner  
    1.0f, 0.0f,  // lower-right corner
    0.5f, 1.0f   // top-center corner
}
```
### texture wraping
```
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_MIRRORED_REPEAT);
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_MIRRORED_REPEAT);
```
1. 第一个参数说明材质的样式：是一个2D材质
2. 第二个参数是材质的坐标轴。s,t,r相当于x,y,z
3. 第三个参数设置材质的重复规律，材质坐标范围$[-1.0, 1.0]$，如果超过这个范围将会重复材质
	1. GL_REPEAT
	2. GL_MIRROREN_REPEAT
	3. GL_CLAMP_TO_EDGE
	4. GL_CLAMP_TO_BORDER
		1. 使用需要进一步操作
			1. `float borderColor[] = { 1.0f, 1.0f, 0.0f, 1.0f };`
			2. `glTexParameterfv(GL_TEXTURE_2D, GL_TEXTURE_BORDER_COLOR, borderColor);`
	5. ![[Pasted image 20240925162413.png]]


### texture filtering
材质的渲染方式
1. GL_NEAREST：多个texture unit采用最近取样的方式
	1. ![[Pasted image 20240925162923.png]]
	2. 一样的颜色
2. GL_LINEAR：仿射取样
	1. ![[Pasted image 20240925162950.png]]
	2. 线性组合、
3. ![[Pasted image 20240925163039.png]]
	1. 第一个颜色鲜明，像素感高
	2. 第二个颜色模糊，更加光滑
```
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_NEAREST); glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
```


### Mipmap
远的模型在屏幕上很小，如果还采用复杂的渲染将会浪费性能
于是OpenGL可以先预制材质的远材质，采用长宽一半的方式加载多个
![[Pasted image 20240925163333.png]]
```
glGenerateMipmap(GL_TEXTURE_2D);
```
各个MipMap之间的连接方式
```
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR_MIPMAP_LINEAR); glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
```

### load texture
用stb库。通过宏定义的方式，启用库中函数实例。
```
#define STB_IMAGE_IMPLEMENTATION 
#include "stb_image.h"
```
使用的基本流程
```c++
unsigned int texture;
glGenTextures(1, &texture);
glBindTexture(GL_TEXTURE_2D, texture);
// set the texture wrapping/filtering options (on the currently bound texture object)
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_REPEAT);	
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_REPEAT);
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR_MIPMAP_LINEAR);
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
// load and generate the texture
int width, height, nrChannels;
unsigned char *data = stbi_load("container.jpg", &width, &height, &nrChannels, 0);
if (data)
{
    glTexImage2D(GL_TEXTURE_2D, 0, GL_RGB, width, height, 0, GL_RGB, GL_UNSIGNED_BYTE, data);
    glGenerateMipmap(GL_TEXTURE_2D);
}
else
{
    std::cout << "Failed to load texture" << std::endl;
}
stbi_image_free(data);
```
1. `stbi_load()`函数
	1. 返回的是图片的矩阵
	2. 第一个参数是图片的位置
	3. 接下来是长、宽、channel
2. `glTexImage2D`函数就是用来绑定实际内容的函数
	1. 第一个参数：二维图片
	2. 第二个 参数Mipmap的lever，0为原本的图片
	3. 第三个参数：用什么格式渲染
	4. 然后就是长、宽
	5. alway 0
	6. 图片的实际格式
	7. 图片的数据类型
	8. 图片数据

### Applying texture
```
float vertices[] = {
    // positions          // colors           // texture coords
     0.5f,  0.5f, 0.0f,   1.0f, 0.0f, 0.0f,   1.0f, 1.0f,   // top right
     0.5f, -0.5f, 0.0f,   0.0f, 1.0f, 0.0f,   1.0f, 0.0f,   // bottom right
    -0.5f, -0.5f, 0.0f,   0.0f, 0.0f, 1.0f,   0.0f, 0.0f,   // bottom left
    -0.5f,  0.5f, 0.0f,   1.0f, 1.0f, 0.0f,   0.0f, 1.0f    // top left 
};

glVertexAttribPointer(2, 2, GL_FLOAT, GL_FALSE, 8 * sizeof(float), (void*)(6 * sizeof(float)));
glEnableVertexAttribArray(2); 
```
VertexAttribPointer
![[Pasted image 20240925165142.png]]

#### vertexshader要修改
```
#version 330 core
layout (location = 0) in vec3 aPos;
layout (location = 1) in vec3 aColor;
layout (location = 2) in vec2 aTexCoord;

out vec3 ourColor;
out vec2 TexCoord;

void main()
{
    gl_Position = vec4(aPos, 1.0);
    ourColor = aColor;
    TexCoord = aTexCoord;
}
```

#### fragShader要修改
```
#version 330 core
out vec4 FragColor;
  
in vec3 ourColor;
in vec2 TexCoord;

uniform sampler2D ourTexture;

void main()
{
    FragColor = texture(ourTexture, TexCoord);
}
```
1. 为什么要将TexCoord设置为uniform
	1. 方便进行同一个模型，不同擦之

#### 使用
```
glBindTexture(GL_TEXTURE_2D, texture);
glBindVertexArray(VAO);
glDrawElements(GL_TRIANGLES, 6, GL_UNSIGNED_INT, 0);
```

### Texture Units
在vertexshader中我们将sample2D设置为uniform可以用来绑定多个材质，或者换材质
```
shader.use();
glUniform1i(glGetUniformLocation(shader.ID, "texture0"), 0);
glUniform1i(glGetUniformLocation(shader.ID, "texture1"), 1);
```
1. `glUniform1i`的第二个参数
	1. 0表示texture内存中第0个texture，以此类推
2. 在重新绑定uniform变量前要使用`shader.use()`
渲染的代码将如下进行更新
```
glActiveTexture(GL_TEXTURE0);
glBindTexture(GL_TEXTURE_2D, texture0);
glActiveTexture(GL_TEXTURE1);
glBindTexture(GL_TEXTURE_2D, texture1);
```
出来的效果如下，因为opengl认为在y轴上，0.0表示的是图像的底部。
![[Pasted image 20241012104442.png]]
使用stb库中函数进行翻转`stbi_set_flip_vertically_on_load(true)`

