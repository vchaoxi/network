# udp网络程序-发送数据

创建一个udp客户端程序的流程是简单，具体步骤如下：

1.创建客户端套接字

2.发送/接收数据

3.关闭套接字

![](/assets/02-就业班-02-1.jpg)

代码如下：

```python

import socket

# 1. 创建套接字
udpSocket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

# 2. 准备接收方的地址
#sendAddr = ('192.168.5.65', 8008)
sendAddr = ('127.0.0.1', 8008)

# 3. 从键盘获取数据
sendData = input("请输入要发送的数据:")

# 4. 发送数据到指定的电脑上
udpSocket.sendto(sendData.encode(), sendAddr)

# 5. 关闭套接字
udpSocket.close()
```

