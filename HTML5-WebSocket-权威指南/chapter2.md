# WebSocket API   

## 2.1 WebSocket API 概述   

    . WebSocket 连接是在客户端和服务器第一次握手时将http协议升级为websocket协议来完成，这一工作在同样的底层TCP连接上进行。   
    . 一旦websocket连接建立，就可以通过websocket api定义的接口来传递 websocket消息了。  
    . websocket api 是完全事件驱动的，这意味着不需要通过轮询的方式来获取目标资源的最新状态，只需在客户端监听需要的通知和更改即可。    

## 2.2 WebSocket API 入门   

    websocket api 让我们可以通过 web, 在客户端应用程序 和 服务器端进程之间建立全双工的双向通信。它规定了可用于客户端的方法及客户端与网络的交互方式。   
    . 首先，需要调用websocket构造函数建立websocket连接。    
    . 该构造函数返回一个对象，可以监听该对象上的事件.   
    . 这些事件告诉我们何时连接建立，何时消息到达，何时出现错误，何时连接关闭。    
    . 也可以和构造函数返回的对象进行交互，发送消息或关闭连接。  

### 2.2.1 WebSocket 构造函数   
    
    new WebSocket(url, [protocols])   

### 2.2.2 WebSocket 事件  

    和所有web api一样，websocket 事件监听方式有两种：方法：addEventListener, 属性： on + <event名称>   
    open, message(文本字符串，二进制-blob,arraybuffer), error, close   


### 2.2.3 websocket 方法： send（只能在open之后，close之前发送）， close(code, reason)      

### 2.2.4 websocket 对象特性： readyState, bufferedAmount, protocol     

## 2.5 在 websocket 中使用html5 多媒体 （依赖于可以传递二进制数据）   
 

