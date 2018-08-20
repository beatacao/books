# BOM  

    BOM（浏览器对象模型），由于一直依赖没有事实上规范，导致各个浏览器提供商对BOM都有自己的扩展，因此各个浏览器共有的对象即成为事实的标准。  本章主要内容：  
    window 对象，location(页面信息)，navigator(浏览器信息)，控制窗口、框架和弹出窗口。  

## 8.1 window 对象  

    . BOM 的核心对象  
    . window对象是浏览器的一个实例:（Object.getPrototypeOf(window) === Window.prototype // true  
    . 双重身份：ECMAScript 的 Global对象；js访问浏览器的接口； 

### 8.1.1 全局作用域  
    
> . 因为是ECMASCcript中的Global对象，因此，所有在全局作用域中声明的变量和函数都是window对象的属性和方法。 

> . 定义全局变量和在window对象上直接定义属性是有区别的：  

    var a = 10  
    window.b = 20  
    c = 30  
    delete window.a  //并没有删除，返回false  
    delete window.b  //删除成功，返回true  
    delete window.c  //删除成功，返回true  
    window.a    //10   
    window.b    //undefined    
    window.c    //undefined  

    以上现象原因是因为直接在window对象上定义的属性，[[configurable]]为true, 通过全局变量定义的变量[[configurable]]为false.  [[configurable]] 为false, 不可删除  

> 直接访问未声明的全局变量会报错，通过 window.xxx 属性形式则不会报错

### 8.1.2 窗口关系和框架  

    . frameset 和 frame 在 html5 中已废弃  
    . frameset 和 frame 与 iframe 的区别  
    . 全局作用域中 self === window  
    . 窗口关系： top, window, self, frames[index], frames[name], parent  

### 8.1.3 窗口位置  

    . screenX, screenY, screenTop, screenLeft 
    . moveTo , moveBy 

### 8.1.6 间歇调用和超时调用  

    当需要严格的按照先后顺序依次间歇执行某段代码时，一般使用超时调用递归（setTimeout）模拟间歇调用，不直接使用间歇调用（setInterval）, 因为间歇调用的下一次执行不一定在上一次执行完成之后。  

### 8.1.7 系统对话框  

    alert, confirm, prompt (返回值)：这几个都是同步对话框   
    window.print, window.find: 异步对话框  

## 8.2 loaction 对象   

    . window.location 和 document.location 指向的是同一个对象。  
    l. ocation.assign(url) 等同于 location.href = url 和 window.location = url
    . 设置location的各个属性（protocal, hostname, host, pathname, search, hash-不会重新加载），会导致页面重新加载并生成一个新的历史记录（回退）， 使用 location.replace 不可回退  
    . location.reload 如果不设置任何参数，会以最有效的方式重载页面，比如可能会从缓存中重载；如果想要页面始终从服务器重新加载，传入参数 true: location.reload(true)  

## 8.3 navigator 对象

    . 主要包含浏览器相关信息。与其他BOM对象的情况一样，navigator对象也有一套自己属性。通常用于检测浏览器类型。  
    . 一般检测浏览器类型用 navigator.userAgent 和 对某特性的支持程度做检测。  
    . navigator.appName 为了 DOM0 兼容问题，一般会返回 netscape ，所以不能用于浏览器类型检测。  

### 8.3.1 检测插件  

> 非IE浏览器：navigator.plugins, 插件为 MimeType类型

    function hasPlugin(name){  
        var plugins = navigator.plugins  //类似数组对象，但不能用数组方法，比如some  
        for(var i in plugins){  
            if(plugins[i].name.toLowerCase().indexOf(name)>-1){  
                return true  
            }  
        }  
        return false  
    }  

> IE 浏览器  

    IE浏览器不使用Netscape式插件，IE使用COM对象的方式实现插件，而COM对象使用唯一标志符来标识，因此，检测IE中的插件，必须知道插件的COM标识  

    function hasIEPlugin(name){   
        try{  
            new ActiveXObject(name)  // ActiveXObject是微软为JScript添加的一种宿主对象，用于访问COM对象   
            return true   
        }catch(e){   
            return false   
        }   
    }     
    hasIEPlugin('ShockwaveFlash.ShockwaveFlash')      

> navigator.plugins.refresh(true/false)   

### 8.3.2 注册处理程序   

    设置web应用程序作为某个协议处理器。navigator.registerProtocolHandler().   
    参考： https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator/registerProtocolHandler/Web-based_protocol_handlers   
## 8.4 screen 对象  

    浏览器外部屏幕信息。一般用于客户端能力的站点跟踪工具中。  
    和其他BOM对象一样，有一套属于自己的属性（width, height, availWidth, availHeight等）

## 8.5 history对象  

    浏览器历史记录，处于安全考虑，开发人员无法通过history访问用户浏览的历史记录。  
    history一般用于创建自定义的‘前进’和‘后退’，或检测当前页面是不是用户历史记录中第一个页面（history.length === 0）  


