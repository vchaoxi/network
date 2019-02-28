# udp应用：聊天室

## 1. 运行现象

测试客户端

![](/assets/Snip20160901_76.png)

聊天室端

![](/assets/Snip20160901_75.png)

## 2. 参考代码

```python

import socket
from time import ctime

# 1. 创建套接字
udpSocket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

# 2. 绑定ip和端口
bindAddr = ('', 7788)  # ip地址和端口号，ip为空表示本机任何一个ip
udpSocket.bind(bindAddr)

while True:
    # 3. 等待接收对方发送的数据
    recvData = udpSocket.recvfrom(1024)  # 1024表示本次接收的最大字节数

    # 4. 打印信息
    print(f'[{ctime()}] {recvData[1][0]}:{recvData[0].decode()}')

# 5. 关闭套接字
udpSocket.close()
```

