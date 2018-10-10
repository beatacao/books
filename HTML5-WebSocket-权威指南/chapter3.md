# WebSocket 协议   

    协议： 协议是计算机中最重要的部分之一。他们跨越编程语言，操作系统和硬件体系解构，允许不同人编写，不同机构操作的组件跨越房屋甚至在全球范围内通信。开放，可互操作系统中的许多成功案例，都归功于精心设计的协议。   
    WebSocket 是定义服务器和客户端如何通过Web通信的一种网络协议。   

## 3.1 WebSocket 协议之前   

    TCP/IP： IP（Internet Protocol 网络协议），负责在互联网的两台主机之间传递数据封包。 TCP(Transmission Control Protocol, 传输控制协议)：可以跨域互联网，在两个端点之间可靠地双向传输字节流的一个管道。  

### 3.1.1 互联网简史   

    . 一开始，互联网主机之间通过TCP/IP协议进行通信，在这种情况下，任何主机都可以建立新的连接。   
    . 一旦TCP连接建立，两台主机可以在任何时候发送数据。 --------- 需要对 TCP/IP 协议详细了解。   
    . 你想在网络协议中实现的其他功能，必须在传输协议的基础上构建，这些更高的层次，被成为应用层协议（如IRC, Telnet, HTTP. WebSocket等）    

### 3.1.2 Web 和 HTTP 

    . Web 是使用URL(Universal 统一资源定位符)链接的超文本文档系统。    
    . Web 变得越来越流行的同时，NAT(network address translation, 网络地址转换)，HTTP代理，防火墙等也越来越常见。许多互联网用户都没有公开的IP地址，用户并不都有唯一的IP地址，这些问题都妨碍了可寻址性。   
    . 占有统治地位的HTTP，并不要求客户端具有可寻址性，它可以很好地利用客户端应用程序驱动的交互，因为所有请求都是由客户端发起的。   
    . 本质上，HTTP内置的文本支持，URL 和 HTTPS 使 Web 成为可能，但某种程度上，HTTP 造成了互联网的退化，因为HTTP不需要可寻址的客户端，Web世界的寻址变成不对称的。浏览器能够通过URL找到服务器资源，但服务器应用程序却无法主动向客户端发送资源。客户端只能发送请求，服务器只能相应未解决的请求。在这个非对称的世界中，要求全双工通信的协议无法正常工作。   
    . WebSub: 前称 PubsubHubbub   

    HTTP 特点： URL， http安全性，内置文本支持   

## 3.2 WebSocket 简介   

### 3.2.1 websocket: web 应用程序的互联网能力    

    . 和 TCP 一样，WebSocket 是异步的，可以用作高级协议的传输层。（HTTP是用于文本传输的简单的同步请求 - 响应式协议）  
    . WebSocket 为 Web应用程序保留了 HTTP特性的同时，提供了 TCP风格的网络能力。寻址仍然是单向的，服务器可以异步发送给客户端数据，但是只在 websocket连接打开时才可以。在客户端和服务器之间，websocket连接始终打开。 websocket 服务器也可以作为websocket客户端。   
    . 网络模型：OSI(开放系统互连 open systems interconnection) - 在互联网出现之前所遵循的模型(7层)。 TCP/IP: 在互联网出现之后，为互联网所设计的网络模型（4层）  
    . 查看流量： wireshark, tcpdump   

## 3.3 websocket 协议   

## 3.4 用 Node.js 编写 WebSocket 服务器   

    const srv = http.createServer( (req, res) => {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('okay');
    });
    srv.on('upgrade', (req, socket, head) => {
        socket.write('HTTP/1.1 101 Web Socket Protocol Handshake\r\n' +
                    'Upgrade: WebSocket\r\n' +
                    'Connection: Upgrade\r\n' +
                    '\r\n')
    })

> 构建远程 js 控制台  - repl 

    
