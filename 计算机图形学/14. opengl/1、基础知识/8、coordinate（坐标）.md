### 坐标分类
1. Local space
	1. local space通过 modelmatirx转换为world space
![[Pasted image 20241104220013.png]]
1. world space
	1. world space 通过viewmatrix转换为view space（相机坐标系）
![[Pasted image 20241104220138.png]]
2. view space
	1. view space通过projectionMatrix转换为带有透视效果的clip space
![[Pasted image 20241104220149.png]]
4. clip space
![[Pasted image 20241104220256.png]]
6. screen space

### frustum（截面体）
1. 在截面椎体中的面将会被保存
2. 在截面椎体外的面将会被舍去
3. 对截面椎体进行标准化操作，使得椎体可以在-1到1然后在窗口显示
4. frustum是实际空间中的一个空间，然后opengl将三维物体画到二维图像上，最左边的顶点是-1,最右边是1,最上是1,最下是-1.

### orthographic projection
![[Pasted image 20241105222854.png]]
1. 正交投影的frustum是一个长方体
2. 所以`glm::ortho()`涉及参数有六个
	1. left
	2. right
	3. bottom
	4. top
	5. near
	6. far

### perspective projection
![[Pasted image 20241105230255.png]]
1. 透视投影的frustum是一个截面椎体
2. `glm::perspective()`有4个参数
	1. 第一个参数`glm::radians(45.0f)
	2. 第二个参数`width/height(窗口的宽长比)`
	3. 第三个参数`near`
	4. 第四个参数`far`

### vertexShader
```
#version 330 core

layout (location = 0) in vec3 Pos;

uniform mat4 model;
uniform mat4 view;
uniform mat4 projection;

out vec2 TexCoord;

void main(){
    gl_Position = projection * view * model * vec4(Pos, 1.0f);
	TexCoord = vec2(inTexCoord.x, inTexCoord.y);
}
```
