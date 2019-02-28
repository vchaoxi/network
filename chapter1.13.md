# udp应用：echo服务器

## 1. 运行现象

测试客户端

![](/assets/Snip20160901_74.png)

echo服务器端

![](/assets/Snip20160901_73.png)

## 2. 参考代码

```python

import socket

# 1. 创建套接字
udpSocket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

# 2. 绑定ip和端口
bindAddr = ('', 7788)  # ip地址和端口号，ip为空表示本机任何一个ip
udpSocket.bind(bindAddr)

num = 1
while True:
    # 3. 等待接收对方发送的数据
    recvData = udpSocket.recvfrom(1024)  # 1024表示本次接收的最大字节数

    # 4. 将接受到的数据再发送给对方
    udpSocket.sendto(recvData[0], recvData[1])

    # 5. 统计信息
    print(f'已经将接收到的第{num}个数据返回给对方，内容为：{recvData[0].decode()}')
    num += 1

# 6. 关闭套接字
udpSocket.close()

```


