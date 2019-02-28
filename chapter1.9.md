# udp网络程序-发送、接收数据

## 1. 创建udp网络程序-接收数据

```python

import socket

# 1. 创建套接字
udpSocket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

# 2. 准备接收方的地址
sendAddr = ('127.0.0.1', 8008)

# 3. 从键盘获取数据
sendData = input("请输入要发送的数据:")

# 4. 发送数据到指定的电脑上
udpSocket.sendto(sendData.encode(), sendAddr)

# 5. 等待接收对方发送的数据
recvData = udpSocket.recvfrom(1024)  # 1024表示本次接收的最大字节数

# 6. 显示对方发送的数据
# print(recvData)
print(recvData[0].decode())

# 7. 关闭套接字
udpSocket.close()

```


