# JSON(Javascript Object Notation Javascript对象表示法)   
```
    JSON是一种表示数据结构的语法，该语法基于javascript(注意与之的区别)
    JSON可以直接转换为javascript对象，操作方便；
    xml需要转换为DOM，再通过DOM操作数据，相比之下就比较繁琐
```
## 语法  
* 对象和数组通常是JSON数据结构的最外层形式  
* 数据类型支持复杂数据结构（对象，数组），简单值（字符串，数值，null, 布尔值）
* JSON数据类型不支持undefined, 变量，函数和对象实例   
* 复杂数据结构：属性必须用双引号括起来，最后一个属性后不能有逗号
* 数值类型：序列化会自动忽略前导零，解析对于前导零会报错；如果有小数点，后面至少跟着一位数字
* 字符串：有一些特殊字符串，js语法不支持（需要转义符转义），JSON对象支持 
* 不是javascript语言特有  

## 解析和序列化
* 开始用eval来解析，缺陷：有安全隐患，可能会执行恶意代码    
* ECMAScript5 对解析和序列化JSON进行了规范，定义了全局对象JSON (IE8+, Firefox3.5+, Chrome等高版本浏览器均支持，不支持的浏览器使用shim)   
* 序列化支持过滤器（数组，函数），格式定义，toJSON方法
```
    序列化参数执行顺序：
    1、如果存在toJSON方法并能通过它取得有效值，调用该方法，否则返回对象本身   
    2、如果提供了第二个参数，应用该过滤器。传入函数过滤器的值是1返回的值
    3、对2返回的每个值进行相应的序列化
    4、如果提供了第三个参数，执行相应的格式化
```
* 解析同样支持第二个参数，该参数为一个函数，函数签名和序列化第一个过滤函数签名一样（只不过序列化过滤函数被称为替换replacer, 解析第二个函数参数称为还原函数reviver）

# 参考资料
* https://bestiejs.github.io/json3/
* https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/JSON
* 关于特殊字符： http://landcareweb.com/questions/36739/json-stringifyhe-u2028-u2029-jian-cha