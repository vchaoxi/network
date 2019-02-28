# tcp客户端

tcp客户端，并不是像之前一个段子：一个顾客去饭馆吃饭，这个顾客要点菜，就问服务员咱们饭店有客户端么，然后这个服务员非常客气的说道：先生 我们饭店不用客户端，我们直接送到您的餐桌上

如果，不学习网络的知识是不是 说不定也会发生那样的笑话 ，哈哈

所谓的服务器端：就是提供服务的一方，而客户端，就是需要被服务的一方

# tcp客户端构建流程

tcp的客户端要比服务器端简单很多，如果说服务器端是需要自己买手机、查手机卡、设置铃声、等待别人打电话流程的话，那么客户端就只需要找一个电话亭，拿起电话拨打即可，流程要少很多

示例代码：

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

    # 3. 发送数据/接收数据
    send_data = input('请输入要发送的数据:')
    tcp_socket.send(send_data.encode())

    recv_data = tcp_socket.recv(1024)
    print(f'接收到的数据为:{recv_data.decode()}')

    # 4. 关闭套接字
    tcp_socket.close()


if __name__ == '__main__':
    main()

```

## 运行流程：

### tcp客户端

![](/assets/tcp_client.png)

### 网络调试助手：

![](/assets/ass_server.png)

