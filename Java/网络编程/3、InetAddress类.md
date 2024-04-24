1. 获取本机InetAddress对象，利用静态工厂方法
```
 InetAddress localHost=InetAddress.getLocalHost();
```
2. 根据指定的主机名获取InetAddress对象
	1. 会throw UnKownnHostException
	2. 可域名可ip
```
InetAddress localhost=InetAddress.getByName();
```
3. 获取多个InetAddress对象
```
InetAddress localhosts[]=InetAddress.getAllByName();
//可能www.xxxx.com有两个主机地址
```
5. 通过InetAddress对象获取
	1. 查询ip
		1. getHostAddress();返回一个ipv4地址字符串
		2. getAddress();返回一个ipv4的byte数组
	2. 查询主机名
		1. getHostName():域名或主机名,不知道主机名字才会查询DNS
		2. getCanonicalHostName();一定会查询DNS
	3. bool isMulticastAddress();判断是否是一个多播地址