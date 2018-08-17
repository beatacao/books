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