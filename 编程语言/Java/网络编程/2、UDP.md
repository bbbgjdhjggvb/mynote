#### 客户端
代码框架
```
1.建立一个Socket
DatagramSocket socket=new DatagramSocket();//随机端口
2.创建一个包
InetAddress localhost=InetAddress.getByName("127.0.0.1");
int port=8080;
String message="";
DatagramPacket packet=new DatagramPacket(message,lenth,localhost,port)
3.发送包
socket.send(packet);
4.结束流
socket.close();
```
1. DatagramPacket的构造参数
	1. byte数组
	2. 长度
	3. 目的地址
	4. 目的端口
#### 服务端
代码框架
```
1. 监听端口
DatagramSocket socket=new DatagramSocket(8080);
2. 创建包用来接收
byte[] buffer=new byte[1024];
DatagramPacket packet=new DatagramPacket(buffer,0)
3. 接收
socket.receive(packet);
String str=new String(packet.getData(),0,packet.getLength());
4. 关闭资源
socket.close();
```
