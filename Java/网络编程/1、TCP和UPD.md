#### TCP网络编程
创建服务端
1. 创建ServerSocket，监听端口
```
ServerSocket serversocket=new ServerSocket(8090);
如果8090端口已经被其他程序监听，那么将会异常
```
2. 等待连接
```
Socket socket=serversocket.accept();
如果没有连接，程序会阻塞在这一行代码
```
创建客户端
1. 连接上服务器
```
Socket socket=new Socket(InetAddress.getXXXX(),端口);
```