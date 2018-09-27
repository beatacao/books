# HTML5 WebSocket简介   

## 1.2 html5 连接性  

    . 跨文档消息传递(跨域通信)： postMessage(仅仅是前端概念，文档之间跨域通信，涉及到和后端通信方面，就无能为力了)
    . websocket   
    . 服务器发送事件Server-sent Event: EventSource    

## 1.3 旧的HTTP架构概览  

> 在HTTP1.0 和 HTTP1.1中，低效的根源：   
    1、HTTP 用于文档共享，而不是丰富的交互性应用程序。而我们在桌面上习以为常的交互，已渐渐进入web.  
    2、随着web应用程序的交互复杂度提高，HTTP在客户端和服务器端通信所需的信息量大大增加。   
    3、HTTP无状态特性造成重复传递头信息，宽带浪费  
    4、半双工，通信效率低   

> web 即时通信技术 

    . 轮询： 如果知道精准的信息更新间隔，轮询比较合适。否则：请求浪费，并不实时
    . comet 技术：（长轮询和流）   
        . 长轮询： 如果信息量较大，也会造成宽带浪费。另一个问题： 没有标准支持。 
        . iframe流： 服务器从不发出完成http响应的请求，从而使连接一直保持打开。对于有防火墙或反向代理的架构模式，由于防火墙和反向代理有可能缓存响应，因此会造成更严重的信息延迟。
    . SSE(server-sent event)     
    . websocket  

## 1.4 websocket 入门   

    为解决已有web即时通信技术的问题，html5规范在连接性部分包含了 WebSocket. WebSocket是一种全双工，双向，单套接字连接。  
    区别与http请求，websocket 请求，只有一个请求，并且从客户端到服务端，和服务端到客户端都会重用这一个连接。  

## 1.5 为何 websocket   

    . 性能： 降低延迟；减少请求数和重复的请求头信息   
    . 简洁   
    . 标准  
    . http 不适合即时通信   

## 1.6 websocket 和 RFC 6455 (RFC 征求意见稿)   

    WebSocket 是协议，WebSocket API是一系列接口，供应用程序控制 WebSocket 协议； API由 W3C 编写；协议由 IETF 编写。    
    WebSocket 能通过 Web 实现客户端和服务器之间的全双工双向通信，并且支持二进制数据和文本字符串的传输。   


### webRTC SPDY