# chapter4 用 XMPP(标准聊天协议) 构建 WebSocket 上的即时消息和聊天   

## 4.1 协议分层  

    TCP, TLS/TCP(TLS 位于 TCP 上层，安全传输 - https, wss)
    WebSocket, HTTP
    XMPP(xExtensible Messaging and Presense Protocol, 可扩展消息与现场处理协议), STOMP（Simple Text Oriented Messaging Protocol, 面向简单文本的消息协议）

## 4.2 XMPP(标准聊天协议)： XML 的流化   

    . XMPP 中 X 代表可扩展，这个可扩展意味着，使用 XML 扩展机制创建命名空间。   
    . XML 是文档格式， XMPP是协议，XMPP 是如何将文档语法用于通信的，以下两种方式： 
        . 将每条信息单独当做一个文档发送除去 -- 出现不必要的冗长文档   
        . 将对话当做一个长文档，随着时间推移和消息传输而增长，这是 XMPP 对文档语法的处理方式。在这种方式下，在 XMPP 连接期间，双向对话的各方都由一个流化的 XML 文档表示，该文档在连接中断时结束。该流化文档的根节点由 <stream/> 表示。流的最高级子节点是该协议的单独数据单位，称作‘节’。
    . 流中的 节 与websocket消息的对齐   

## 4.3 通过 websocket 构建聊天和即时消息应用程序   

    server: https://github.com/dhruvbird/node-xmpp-bosh    
    client: https://github.com/strophe/strophejs    



