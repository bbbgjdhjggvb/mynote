1. 获取本机InetAddress对象
```
 InetAddress localHost=InetAddress.getLocalHost();
```
2. 根据指定的主机名获取InetAddress对象
```
InetAddress localhost=InetAddress.getByName();
```
3. 根据域名
```
InetAddress baidu=InetAddress.getByName("www.baidu.com");
返回：域名/ip
```
4. 通过InetAddress对象获取
```
getHostAddress()
getHostName():域名或主机名
```