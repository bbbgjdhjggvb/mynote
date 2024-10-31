
string str="xxxxxx"
```
str.find(substr,pos);没有返回-1，如果有返回第一次处出现的索引位置,从左往右找
str.rfind(substr,pos);从右往左找
str.replace(pos,lenth,str);将从pos开始的lenth个字符替换为str
str.insert(pos,str);//索引后插入
str.substring(pos,len)
```
append与+=区别
```
+="xxxxx";
+='x';
+=str;
append(const char *s)
append(str)
```
### C语言字符数组操作
1. strcpy
	1. 返回char*
	2. strcpy（dest，src）
	3. 要保证dest的空间足够的大
	4. 会将src的'\\0'拷贝到dest
2. strcat
	1. 返回char*
	2. strcat（dest，src）
	3. 要保证dest的空间足够的大
	4. src和dest都要有'\\0'
3. strcmp
	1. 正数：左大于右
	2. 0：左等于右
	3. 负数：左小于右
4. strstr
	1. 返回字符串str2在str1中第一次出现的位置
	2. strstr(str1,str2)
<<<<<<< HEAD


#### 利用流操作来实现string的split函数

```
std::vector<std::string> split(const std::string &s, char delimiter){
	std::vector<std::string> res;
	std::stringsteam ss(s);
	std::string item;

	 while(std::getline(ss,item,delimiter)){
		 res.push_back(item);
	 }
	 return res;
}
```

#### find和substring实现
```
int end = s.find(delimter);

while(end != -1){
	res.push_back(str.substr(start, end-start));
	start = end + delimter.size();
	end = str.find(delimter, start);
}

res.push_back(str.substr(start));
```
处理小文本时，考虑使用第一种

#### 利用equals实现判断前缀
```
#include <algorithm>

std::equals(s.begin(), s.end(), os,begin());自动比较begin到end这个范围，不管os的长度是多少
```

#### 将string转换成const char *
```
const char * xxx = xxxstr.c_str();
```

#### 将int转换为string
```
string s_num = std::to_string(num)
```
