# 应用：模拟QQ聊天

## 客户端参考代码

```python

import socket


def main():
    # 1. 创建tcp的套接字
    tcp_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

    # 2. 连接服务器
    server_ip = input('请输入要连接的服务器IP:')
    server_port = int(input('请输入要连接的服务器端口:'))
    server_addr = (server_ip, server_port)
    tcp_socket.connect(server_addr)

    while True:
        # 3. 发送数据/接收数据
        send_data = input('send: ')
        if len(send_data) > 0:
            tcp_socket.send(send_data.encode())
        else:
            break

        recv_data = tcp_socket.recv(1024)
        print('recv:', recv_data.decode())

    # 4. 关闭套接字
    tcp_socket.close()


if __name__ == '__main__':
    main()

```

## 服务器端参考代码

```python

import socket


def main():
    # 创建socket
    tcp_server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

    # 绑定本地信息
    address = ('', 7788)
    tcp_server_socket.bind(address)

    # 使用socket创建的套接字默认的属性是主动的，使用listen将其变为被动的，这样就可以接收别人的连接了
    tcp_server_socket.listen(5)

    while True:
        # 如果有新的客户端来链接服务器，那么就产生一个新的套接字专门为这个客户端服务器
        # new_socket用来为这个客户端服务
        # tcp_server_socket就可以省下来专门等待其他新客户端的连接
        new_socket, client_addr = tcp_server_socket.accept()

        while True:
            # 接收客户端发送过来的数据，最大接收1024个字节
            recv_data = new_socket.recv(1024)
            # 如果接收的数据长度为0，意味着客户端已经关闭了连接
            if len(recv_data) > 0:
                print('recv:', recv_data.decode())
            else:
                break

            # 回送一些数据到客户端
            send_data = input('send: ')
            new_socket.send(send_data.encode())

        # 关闭为这个客户端服务的套接字，只要关闭了，就意味着为不能再为这个客户端服务了，如果还需要服务，只能再次重新连接
        new_socket.close()

    # 关闭监听套接字，只要这个套接字关闭了，就意味着整个程序不能再接收任何新的客户端的连接
    tcp_server_socket.close()


if __name__ == '__main__':
    main()

```

