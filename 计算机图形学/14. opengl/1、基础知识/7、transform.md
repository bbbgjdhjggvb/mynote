大部分需要使用的glm函数可以定义在如下头文件
```
#include <glm/glm.hpp>
#include <glm/gtc/matrix_transform.hpp>
#include <glm/gtc/type_ptr.hpp>
```

### 平移变化
1. 平移矩阵
	1. ![[Pasted image 20241015211636.png]]
例如对一个向量进行平移操作
```c++
glm::vec4 vec(1.0f, 0.0f, 0.0f, 1.0f);
glm::mat4 trans = glm::mat4(1.0f);
trans = glm::translate(trans, glm::vec3(1.0f, 1.0f, 0.0f));
vec = trans * vec;
```
1. `glm::vec4`是一个列向量
2. `glm::mat4`是一个4 * 4的矩阵，`glm::mat(1.0f)`表示单位矩阵，如果没有1.0f就是一个0矩阵
3. `glm::translate()`函数
	1. 返回`glm::mat4`
	2. 参数：
		1. 第一个参数是一个单位矩阵
		2. 第二个参数是`glm::vec3`表示$T_x, T_y, T_z$

### 旋转变化
1. 旋转矩阵：逆时针角度为正，级联矩阵，左边是第一次变化
	1. 绕x轴
		1. ![[Pasted image 20241015211922.png]]
	2. 绕y轴
		1. ![[Pasted image 20241015211945.png]]
	3. 绕z轴
		1. ![[Pasted image 20241015212001.png]]
```c++
glm::mat4 trans = glm::mat4(1.0f);
trans = glm::rotate(trans, glm::radians(90.0f), glm::vec3(0.0, 0.0, 1.0));
trans = glm::scale(trans, glm::vec3(0.5, 0.5, 0.5));  
```
1. `glm::rotate()`
	1. 参数
		1. 第一个：单位矩阵
		2. 第二个：变化角度
		3. 第三个：旋转向量
2. `glm::scale()`
	1. 
### 拉伸变化
1. 变化矩阵
	1. ![[Pasted image 20241015212055.png]]



### shader
```
uniform mat4 transform;

void main()
{
    gl_Position = transform * vec4(aPos, 1.0f);
    TexCoord = vec2(aTexCoord.x, aTexCoord.y);
} 
```
1. 注意是左乘

### 修改uniform变量
```c++
unsigned int transformLoc = glGetUniformLocation(ourShader.ID, "transform");
glUniformMatrix4fv(transformLoc, 1, GL_FALSE,glm::value_ptr(trans));
```