# 译者序  

> HTTP 无状态，半双工

    HTTP 无状态： 即各个http请求之间无上下文衔接，每次请求之间互不影响，无法记忆上次请求。特定场景下可以借助cookie记忆状态。  
        每个http请求都是唯一和独立的。好处：服务器无需记住每次请求的状态，无需存储数据。弊端： 每次请求和响应都会发送关于请求的重复信息； 
           
    HTTP 半双工： 根据通信双方的分工和数据传输方向，通信方式可以分为三种，单工，半双工，全双工

> WebSocket 基于标准，与语言无关，且能在其上任意增加标准的协议层次，从而在HTTP架构中增加了一个全新的传输层。

    全双工，是web 浏览器所用的TCP。   

