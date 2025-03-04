通过物理接口名字来获取ip地址
1. 当一个物理接口绑定一个ip地址时
```
NetworkInterface eth0=new NetworkInterface.getByName("eth0");

```
2. 通过ip地址获取物理接口
```
InetAddress local=InetAddress.getByName("127.0.0.1");
NetworkInterface ni=NetworkInterface.getByInetAddress(local);
```
4. 当一个物理结构绑定多个ip地址时
```
NetworkInterface etho0=NetworkInterface.getByName("eth0");
Enumeration ips=eth0.getInetAddresses();
while(ips.hasMoreElements){
	NetworkInterface ip=ips.nextElements();
	xxxxx
}
```
5. 当要获取多个物理接口ip地址时
```
Enumeration<NetworkInterface> interfaces=NetworkInterface.getNetwork();
```