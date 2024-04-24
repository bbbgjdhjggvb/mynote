#### 1.1 宽字符
加上L前缀的为宽字符，使用UTF-16或者UTF-32编码
```
wchar_t wch=L'你';
wcout对应cout,以此类推
```
#### 1.2 IO对象无拷贝
```
ofstream out1,out2;
out1=out2;错误
函数(out1);错误
```
#### 1.3 输出缓冲
```
cout<<endl;刷新缓冲区，并且换行
cout<<flush;刷新缓冲区，无换行
```
1. unibuf操作符
```
cout<<unitbuf;//接下来无需手动刷新
cout<<"xxx";
cout<<nounitbuf;//回归手动刷新状态
```
#### 1.4 IO类常用函数
由于继承，所以cin,cout相关方法其他IO类也可使用
1. >>
2. <<
3. getline
4. ignore
5. get
6. .str()string流专用，获取流中的string对象