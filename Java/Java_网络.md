 
- 课程源：[p394](https://www.bilibili.com/video/av55246614?p=394) ~[p466](https://www.bilibili.com/video/av55246614?p=466)
---

<!-- TOC -->

- [软件结构](#软件结构)
- [网络通信协议](#网络通信协议)
    - [ICP/IP](#icpip)
- [综合案例： TCP 文件上传案例](#综合案例-tcp-文件上传案例)
    - [UDP](#udp)
- [网络编程三要素](#网络编程三要素)
- [B/S (浏览器/服务器)](#bs-浏览器服务器)

<!-- /TOC -->

---

## 软件结构

    C/S：客户端/服务器 结构
    B/S：浏览器/服务器 结构

## 网络通信协议

    同一网络中的计算机进行连接和通信时需要遵守一定的规则，即网络通信协议

### ICP/IP

    传输控制协议/因特网互联协议 -> IPv4,IPv6 (传输层)

- 面向连接的通信协议：先建立链接
- 三次握手
  - 客户端 -> 服务器:连接请求
  - 服务器 -> 客户端:回应
  - 客户端 -> 服务器:送达去人信息，确认连接
- 保证数据的安全

客户端(Client)
服务器(Server)

步骤：  
   -  服务器端先启动  
   -  服务器不会主动请求客户端  
   -  客户端请求服务器  
   -  客户端和服务器建立连接  
   -  包含一个**IO对象**  
   -  通信数据不仅仅是字符  
   -  所以IO 对象是 **字节流**  

服务器：
- 多个客户端和服务器进行交互，明确每个客户端
  - 在服务器:有accept方法，获取客户端获取请求客户端对象
- 多个客户端和服务器进行交互，就需要使用多个IO对象
  - 服务器没有IO流，服务器可以获取客户端对象Socket
  - 使每个客户端Socket中提供的IO流和客户端进行交互
    - 服务器使用客户端的字节输入流读取客户端发送的数据 (借)
    - 服务器使用客户端的字节输出流给客户端写回数据
- 服务器端：  
    - Socket s1 = server.accept()  //获取客户端对象  192.168.1.1  
    - Socket s2 = server.accept()  // 192.168.1.2

**套接字**：  

    包含IP地址和 端口号的网络单位

**客户端：**

- 构造方法：
  - Socket​(String host, int port)
- 参数
  - String host: 服务器主机名/服务器IP地址
  - int port : 服务器端口号
- 成员函数
  - public InputStream getInputStream()  
                             throws IOException
    - 返回此套接字的输入流
  - public OutputStream getOutputStream()  
                             throws IOException
    - 返回套接字的输出流

- 步骤

  1. 创建一个客户端对象Socket ,绑定IP和端口号
  2. 使用Socket 对象中的方法 **getOutputStream()** 获取字节输出流对象
  3. 使用网络字节输出流对象的方法 write ，给服务器发送数据
  4. 使用Socket对象中的 **getInputStream()** 方法 获取输入流
  5. 使用输入流的 输入对象 read ，读取服务器写回的数据
  6. 释放Socket资源


- 注意：
  1. 客户端和服务器端进行交互，必须使用Socket中提供的网络流，不能使用自己创建的流对象
  2. 当我们创建客户端对象时，会请求服务器，和服务器经过3次握手连接通路，如果服务器没有启动，抛出异常 **ConnectException**

**服务器**

    ServerSocket ：服务器套接字
    读取客户端发送的数据，给客户端写回数据
    表示服务器的类
        java.net.ServerSocket

- 构造方法：
  - public ServerSocket​(int port)
    - throws IOException
  - public ServerSocket​() ： 随机分配 
    - 必须知道是呢个客户端请求的服务器
    - 所以可使用 **accept** 方法获取到请求对象 Socket
    - Listens for a connection to be made to this socket and accepts it. The method blocks until a connection is made.
- 实现步骤
    1. 创建服务器 ServerSocket 对象
    2. 使用 accept方法，获取客户端的套接字 (Socket对象)
    3. 使用Socket对象中的方法 **getInputStream()** 获取输入流
    4. 使用输入流的 输入对象 read ，读取客户端发送的数据
    5. 使用Socket 对象中的方法 **getOutputStream()** 获取字节输出流对象
    6. 使用网络字节输出流对象的方法 write ，给客户端回写数据
    7. 释放资源(Socket ，ServerSocket)

## 综合案例： TCP 文件上传案例

- 原理
  - 客户端读取本地文件，把文件上传服务器，服务器再把文件写入到服务器的硬盘上
- 需求分析
  1. 客户端使用 **本地字节输入流** ，读取要上传的文件
  2. 客户端使用 **网络字节输出流** ，把读取到的文件上传到服务器
  3. 服务器使用 **网络字节输入流** ，读取客户端上传的文件
  4. 服务器使用 **本地字节输出流** ，把读取到的文件，保存到服务器硬盘上
  5. 服务器使用 **本地字节输出流** ，给客户端我会写“上传成功”
  6. 客户端使用 **网络字节输入流** ，读取服务器回写的数据
  7. 释放资源
- 注意：
  - 本地读写使用本地流对象 (本地流)
  - 客户端和服务器之间进行读写，必须使用Socket中提供的字节流对象(网络流)

[Read阻塞及解决方案](https://gitee.com/KawYang/Notes/raw/master/Image/Java/%E7%BD%91%E7%BB%9C_%E4%B8%8A%E4%BC%A0%E6%96%87%E4%BB%B6.png)

### UDP

- 用户数据报协议：无连接的通信协议 
- 耗资小，通信效率高
- 音频、视频、普通数据
- 容易丢失一两个数据包
- 限制在64KB

## 网络编程三要素

1. 协议
2. IP地址
3. 端口号：两个字节组成 0 - 65535之间
    - 1024 之前不能使用
    - 网络软件的端口号不能重复
  - 常用端口号
    - 80：网络端口号 
    - 数据库：
      - mysql：3306
      - oracle：1521
      - Tomcat：8080

## B/S (浏览器/服务器)

  客户端是IE浏览器 ---> 服务器(Java程序) ---> 读取请求信息  ---> 服务器回写信息(网页文件) <文件地址 GET /bilibili/web/index.html HTTP/1.1 >  

  使用BufferedReader 中的ReaderLine 读取一行
  new BufferedReader （new InputStreamReader(is)）


