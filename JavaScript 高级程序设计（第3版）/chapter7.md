# 函数表达式  

    定义函数： 函数声明和函数表达式。函数声明有函数声明提升，函数表达式和普通赋值表达式一样，只有变量提升。   
    
> 不建议以下用法，但可以说明一些问题  

    第一种：  
    if(conditaion){  //这种使用法，不同浏览器会有不同表现，并不总能按照我们期望
        function sayhi(){ console.log('true') }  
    }else{    
        function sayhi(){ console.log('false') }  
    }   
    第二种：  
    var sayhi
    if(conditaion){  //这种使用法，可以按照我们期望
        sayhi = function(){ console.log('true') }  
    }else{    
        sayhi = function(){ console.log('false') }  
    }    

## 7.1 递归函数  

    arguments.callee -- 严格模式下不允许  
    命名函数表达式

## 7.2 闭包  

    . 闭包通常的表现形式是一个函数返回另一个函数。闭包的实现关乎活动对象和作用域链。

    . 作用域链：是在函数创建时生成的，并保存在 [[scope]] 内部变量。闭包函数创建时，被返回函数的作用域链包含了外层函数的活动对象，向上直至全局活动对象。   

    . 活动对象：在函数被调用时，会创建一个执行环境和相应的作用域链。后台的每个执行环境都有一个表示变量的对象 -- 活动对象。 

    . 闭包作用域链：闭包函数在创建时，包含外层函数变量对象（向上直至全局变量对象）的作用域被创建并保存于内部属性 [[scope]] 中，当闭包函数被调用时，会为函数创建一个执行环境，然后通过复制函数[[scope]]属性中的对象构建起执行环境的作用域链。然后，又有一个活动对象被创建并推入当前执行环境作用域链的前端。从而形成闭包调用时的作用域链。   

    . 活动对象的销毁：函数执行过程中，当访问一个变量时，会从作用域链逐层向上查找。一般来讲，函数执行完毕，其执行环境的作用域链被销毁（出于执行环境作用域链最前端的活动对象自然也被销毁）。但，闭包外层函数调用完毕后，该外层函数的执行环境作用域链被销毁，但其活动对象并不会被销毁（仍留在内存中），因为该活动对象被其返回的闭包函数内部属性 [[scope]] 引用。直到闭包函数被销毁，改活动对象才被销毁，其所占用内存得以释放。  

    function outside(){  
        var a = 1, b = 2;   
        return inside(){   
            console.log(a+b)   
        }   
    }   
    var closure = outside()    
    closure()    
    closure = null  //释放内存   

### 7.2.1 闭包与变量  

    闭包保存的是外层函数的整个变量对象，而不是某个变量值。常见的（for ... in 打印列表索引）最能说明这个问题。  

### 7.2.2 关于this  

    . 每个函数在调用时，都会自动获得两个特殊变量： this 和 arguments。内部函数在搜索这两个变量时，只搜索到当前活动对象，因此永远不可能直接访问外部函数的这两个变量。（通常通过把外部函数的这两个变量保存在一个变量中（self）通过作用域链的变量向上查找来访问到）  
    . 匿名函数的执行环境具有全局性。  
    . 赋值表达式的返回值是当前值：  

    var name = 'window'  
    var obj = {  
        name: 'my name',  
        getName: function(){  
            return this.name  
        }  
    }    
    obj.getName()   //my name    
    (obj.getName)()     //my name  
    (obj.getName = obj.getName)()       //window  

### 7.2.3 内存泄露  

    由于IE9之前的版本对Jscript对象 和 COM 对象使用不同的垃圾收集例程。因此，闭包在这些版本会存在一些特殊的问题。具体来说，就是如果闭包作用域链中包含对HTML元素的引用，那么就意味着该元素无法被销毁。  

    // element 无法被销毁  
    function assignHandler(){    
        var element = document.getElementById('xxx')  
        return function(){  
            console.log(element.id)  
        }
    }    

    // 解决  
    function assignHandler(){  
        var element = document.getElementById('xxx')  
        var id = element.id  
        return function(){  
            console.log(id)  
        }  
        element = null  //因为闭包作用域链保存的是外层函数的整个变量对象，所以即便没有引用 element, element 也会被保存在闭包作用域链中无法销毁，需要手动设置为null, 切断与html元素的关联。    
    }   

## 7.3 模仿块级作用域  
> Javascript 无块级作用域（es6 已有），表现：  

    function outputNumbers(){  
        for(var i=0; i<10; i++){  
            console.log(i)  
        }  
        console.log(i)  //9, for中定义的i, 在函数作用域内都可以访问到  
        var i   //js会忽略后续的函数声明  
        console.log(i)  //9  
    }  

> 相关问题原理回顾：  
 1、声明变量时不带var 关键字，该变量即为全局变量。 2、如上述代码，重复定义变量，js会如何处理。  

    可以通过自执行匿名函数来模仿块级作用域。一般用于避免添加多余的全局变量。自执行匿名函数，可以减少闭包占用内存问题。因为没有指向匿名函数的引用，函数执行完毕，就可以立即销毁其作用域链。  

## 7.4 私有变量  






    
