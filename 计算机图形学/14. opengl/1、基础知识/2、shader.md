需要我们进行管理实现的shader有vertex shader和fragment shader，默认实现的有geometry shader和tellellation shader

#### vertex shader
根据输入的点的坐标生成更多的点，以便下一个geometry shader进行连线操作。
1. only precess 3D coordinary where they ‘re between -1.0f to 1.0f on 3 axes。而且值都是float
2. 这些标准坐标值会根据`glViewport`函数的具体像素值进行计算

##### vertex shader模块
```
# version 330 core//表示使用的GLSL（opengl shader language）为3.3版本
layout (location = 0) in vec3 aPos;//layout()这个表示这个vec具有的属性，这里只使用到location属性，并用0来表示location属性，in关键字表示接受的输入vec可以有从1到4，这里只表示三维坐标，并且vertex shader只接受3D coordinary。aPos是这个vec的别名
void main(){
	gl_Postion = vec4{aPos.x, aPos.y aPos.z, 1.0f};
	//vec4的第四个参数通常表示视角
	//gl_Postion是vertex shader的output
}
```

##### compile shader
1. 将模块代码用一个字符指针存储
```
const char *vertexshaderSource = 
"# version 330 core\n"
"layout (location = 0) in vec3 aPos;\n"
"void main(){\n"
"gl_Postion = vec4{aPos.x, aPos.y aPos.z, 1.0f};\n"
"}\0"
//一定要注意\n和\0
```
2. 为shader编译工作在内存上开辟一块空间
```
//create shader是公用函数所以一定要指定是什么类型的shader
unsigned int vertexShader = glCreateShader(GL_VERTEX_SHADER)
```
3. 将这块内存和vertex shader代码进行绑定
```
//第一个参数是内存，第二个参数是要编译的代码的数量，第三个参数是编译的代码，第四个参数不管
glShaderSource(vertexShader, 1 , &vertexShaderSource, NULL);
```
4. 进行编译
```
glCompileShader(vertexShader);
```
5. 检查编译是否通过
```
int success;
glGetShaderiv(vertexshader, GL_COMPILE_STATUS, &success);
if(!success){
	char infolog[512];
	glGetShaderInfolog(vertexshader, 512, NULL, infolog);
	std::cerr << "ERROR: vertex shader compile fail" << infolog <<std::endl;
}
```


#### fragment shader
![[Pasted image 20240908154636.png]]
把光栅化的图形填充色彩
1. shader代码写在字符数组里面
```
const char *fragshaderSource = 
# version 330 core
out vec4 FragColor;

void main(){
	FragColor = vec4{1.0f, 0.5f, 0.2f, 1.0f};//srgb颜色加上透明度
}
```
2. 为编译工作配置空间
```
unsigned int fragmentShader = glCreateShader(GL_FRAGMENT_SHADER);
```
3. 将该空间和shader代码绑定
```
glShaderSource(fragment, 1, &fragshaderSource, NULL);
```
4. 进行编译工作
```
glCompileShader(fragment);
```

#### create shader program
1. 创建shader program
```
unsigned int shaderProgram = glCreateProgram();
```
2. 动态连接shader
```
glAttachShader(shaderProgram, vertexshader);
glAttachShader(shaderProgram, fragmentshader);
glLinkProgram(shaderProgram);
```
3. 检查是否连接成功
```
  
glGetProgramiv(shaderProgram, GL_LINK_STATUS, &success); if(!success) { 
	glGetProgramInfoLog(shaderProgram, 512, NULL, infoLog); 
	... 
}
```
4. 删除为上面shader编译工作开辟的空间
```
glDeleteShader(vertexShader);
glDeleteShader(vertexShader);
```
6. 使用shaderprogram
```
glUserProgram(shaderProgram);
```

#### GLSL
1. begin with version
2. followed by a list of input and output, variables, uniforms
3. and main function
4. vertex的out变量名字必须和fragment的in变量名字相同这样才能链接器shader
##### structure
```glsl
#version version_number
in type var;

	out type var;

uniform type name;

void main(){
	out_var = xxxxx;
}
```

##### type
1. 包含最常用的int，float，double，uint，bool
2. 两个常用容器vector和matrix
##### vector
1. n 代表2，3，4中的一个
2. vecn：默认容纳类型float
3. bvecn
4. ivecn
5. uvecn
6. dvecn
7. 可以使用vec.x, vec.y, vec.z, vec.w去access 各个components
8. 随意组合语法
```c++
vec4 vec = avec.xyxx;
vec4 vec = avec.xxxx + bvec.yyyy;
vec2 ve2;
vec4 vec(ve2, 0 ,0);
```
##### layout、in 和 out
1. layout：说明attribute 数组中具体属性的位置`layout (location = 0) in vec3 aPos`，apos变量在vao中第0位
##### uniform
1. 全局变量，能够在任意shader阶段对这个变量进行定义
2. `glGetUniformLoation(shaderProgram, "outColor")`来获取这个全局变量的位置
3. `glUniform4f(vertexColorLocation, 0.0f, somecolor, 0.0f, 0,0f)`
	1. 由于c不支持重载，所以不同类型函数名字有区分，f：float，i，ui，3f，fv：float vector
4. 


##### 将GLSL文件写入字符数组
```c++
char *readSource(std::string &filename){
	std::ifstream file(filename, std::ios::binary | std::ios::ate);
	if(!file){
		std::cerr<<....
		return nullptr;
	}

	size_t = static_cast<size_t>(file.tellg());
	file.seekg(0, std::ios::beg);

	char *buffer = new char[filesize + 1];
	if(!buffer){
		
	}

	file.read(buffer, filesize);
	if(!file){
		std::cerr<<file.gcount()
		delete
	}

	buffer[filesize] = '\0';
	file.close();
	return buffer;
}
```