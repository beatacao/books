方法：
http认证： 基本认证，摘要认证  

    基本认证： 

        参考：
        https://zh.wikipedia.org/wiki/HTTP%E5%9F%BA%E6%9C%AC%E8%AE%A4%E8%AF%81   
        http://www.cnblogs.com/xiaohuochai/p/6184913.html  

        ps: base64 http协议兼容， 如路由器网页管理接口，没有有效的方式让用户退出？

    摘要认证：    

        参考：
        https://zh.wikipedia.org/wiki/HTTP%E6%91%98%E8%A6%81%E8%AE%A4%E8%AF%81    
        https://www.cnblogs.com/xiaohuochai/p/6189065.html


    https://www.hackingarticles.in/understanding-http-authentication-basic-digest/

oauth   

    参考：  
    https://www.xncoding.com/2017/03/29/web/oauth2.html  
    https://www.jianshu.com/p/a047176d9d65


cookie/session/token 

    参考：   
    https://abigaleyu.co/2017/07/28/cookie-session-token/    
    https://harttle.land/2015/08/10/cookie-session.html    cookie 容易被篡改；session: 防止篡改，但是被盗用后，可以重放   
    https://www.jianshu.com/p/c33f5777c2eb    cookie/session: 有状态（服务器或浏览器端需要一直保存状态），token无状态  
    https://blog.csdn.net/Jmilk/article/details/55686267   session，token优缺点   
    https://segmentfault.com/a/1190000013010835#articleHeader0  


jwt
cas