# 正则表达式

    . 两种创建方式： 字面量， 构造函数。 字面量的使用优先于构造函数；但是构造函数可以动态创建规则；因为在字符串中，反斜杠也表示转义，构造函数创建正则的参数是字符串，所以使用构造函数创建正则时，传入的参数如果需要反斜杠，则需两个反斜杠。  
    .模式：i, g, m(多行模式：^ 即可表示字符串开头，也可表示换行开头； $: 即可表示字符串结尾，也可表示换行结尾)

## 术语与操作符

    . 精准匹配： /test/  
    . [test], [^test], [a-m]  
    . 转义： \[\]\^\-  
    . 开始 ^, 结束： $   
    . 重复出现： ? (0或1次)，+（一次以上），*（0或一次以上）， {n}: n次，{n, m}: n 到m次， {n,}: n次以上
    . 默认重复规则为贪婪模式，添加 ？为非贪婪模式
    . 预定义字符类：有些想要匹配的字符，不能用字面量字符直接表示（如回车这样的控制字符），还有一些常用的想要匹配的字符，正则表达式语法提供了表达这些特殊字符和常用字符的预定义术语。   

        \t, \b, \r, \n, \f, \d, \s, \w, \v, \cA:\cZ, \x0000:\xFFFF, \x00:\xFF, \D, \W, \B, \S
    . 小括号： 双重责任，分组和捕获（capture）, (?:) 不进行捕获
    . 或： |  
    . 捕获反向引用 \n, n表示运行过程中，capture的索引；反向引用一般用于相同字符串的匹配，如：<strong>aabcc</strong> : /<(\w+)>(.+)<\/\1>/

## 正则表达式恩编译 - 创建表达式时编译，每次创建都会编译（为性能考虑，可以尽量减少正则表达式的创建）

## 捕获匹配的结果  
    
    非全局匹配：match
        var str = "filter: alpha(opacity=50);filter: alpha(opacity=50);"
        var reg = /opacity=([^)]+)/
        str.match(reg)   
    全局匹配（match 不返回捕获结果）， 使用 exec(多次调用，每次返回下一个匹配的结果，直至返回null)
        var str = "filter: alpha(opacity=50);filter: alpha(opacity=50);"
        var reg = /opacity=([^)]+)/g  
        reg.exec(str)  //第三次调用会返回null

## 捕获结果的引用   

    两种引用： 正则自身引用（反向引用 \1, \2 ...）, 字符串替换: 'fontFamily'.replace(/([A-Z])/g, '-$1')  
    
## replace(reg, function), 在某程度上可以作为遍历使用   

    例子： foo=1&foo=2&bar=3&bar=4   转换为 foo=1,2&bar=3,4

    var str = 'foo=1&foo=2&bar=3&bar=4'
    var results = []
    var keys = {}
    str.replace(/([^&=]+)=([^&]*)/g, function(full, key, value){
        keys[key] = (keys[key] ? keys[key] + ',' : '') + value
        return ''
    })
    for(var key in keys){
        results.push(key + '=' + keys[key])
    }
    var fomat = results.join('&')

## 利用正则表达式解决的常见问题  

    . 修剪字符串 - 去除头尾空格    
    . 匹配换行符 /.*/  匹配任何非换行符； /[\s\S]*/ 匹配任何字符