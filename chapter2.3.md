# tcp服务器

## 生活中的电话机

如果想让别人能更够打通咱们的电话获取相应服务的话，需要做一下几件事情：

    1.买个手机

    2.插上手机卡

    3.设计手机为正常接听状态（即能够响铃）

    4.静静的等着别人拨打

## tcp服务器

如同上面的电话机过程一样，在程序中，如果想要完成一个tcp服务器的功能，需要的流程如下：

    1.socket创建一个套接字

    2.bind绑定ip和port

    3.listen使套接字变为可以被动链接

    4.accept等待客户端的链接

    5.recv/send接收发送数据

一个很简单的tcp服务器如下：

```python

import socket

# 创建socket
tcp_server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# 绑定本地信息
address = ('', 7788)
tcp_server_socket.bind(address)

# 使用socket创建的套接字默认的属性是主动的，使用listen将其变为被动的，这样就可以接收别人的连接了
tcp_server_socket.listen(5)

# 如果有新的客户端来链接服务器，那么就产生一个新的套接字专门为这个客户端服务器
# new_socket用来为这个客户端服务
# tcp_server_socket就可以省下来专门等待其他新客户端的连接
new_socket, client_addr = tcp_server_socket.accept()

# 接收客户端发送过来的数据，最大接收1024个字节
recv_data = new_socket.recv(1024)
print('接受到的数据为：', recv_data.decode())

# 回送一些数据到客户端
new_socket.send("thank you".encode())

# 关闭为这个客户端服务的套接字，只要关闭了，就意味着为不能再为这个客户端服务了，如果还需要服务，只能再次重新连接
new_socket.close()

# 关闭监听套接字，只要这个套接字关闭了，就意味着整个程序不能再接收任何新的客户端的连接
tcp_server_socket.close()

```

## 运行流程：

### tcp服务器

![](/assets/tcp_server.png)

### 网络调试助手：

![](/assets/ass_client.png)

