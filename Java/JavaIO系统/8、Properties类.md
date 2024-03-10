专门用于读取配置文件的集合类
父类是Hashtable
配置文件的格式必须是key=value
```
Properties properties=new Properties();
//加载配置文件到对象
properties.load(new FileReader(path));
//显示k-v对
properties.list(System.out(PrintStream或PrintWriter))
//根据key获取value
Stringv user=properties.getProperty("user");


//添加新的k-v
1. 添加到对象中
	properties.setPorperty(key,newvalue);
2. 添加到偶文件中
	properties.store(第一个参数是OutputStream或者Writer,String 注释);
//修改k-v
	文件有key就是修改

```