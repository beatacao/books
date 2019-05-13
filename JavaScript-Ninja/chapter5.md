# closure  

    闭包使得函数在任何时候调用时，都可以访问该函数声明时所在作用域。  

## 5.2 使用闭包  

    私有变量；回调和计时器；

## 5.3 绑定函数上下文   

    浏览器事件处理程序（如click事件处理程序）中，默认 this 为当前事件元素；

    if(!Function.prototype.bind){
        Function.prototype.bind = function(oThis){
            if(typeof this !== 'function'){
                throw new Error('Fucntion.prototype.bind - need to be used not be called')
            }

            var aArgs= Array.prototype.slice.call(arguments, 1),
                fn = function(){},
                ftoBound = this,
                boundFn = function(){
                    return ftoBound.apply(ftoBound, aArgs.concat(Array.prototype.slice(aruguments)))
                }
            
            if(this.prototype){
                fn.prototype = this.prototype
            }

            boundFn.prototype = new fn()

            return boundFn
        }
    }

## 5.4 偏应用函数  - 分部函数（curry 函数） 

    Function.prototype.partial = function(){
        var fn = this,
            args = Array.prototype.slice.call(arguments)
        return function(){
            var arg = 0
            for(var i=0; i< args.length && arg < arguments.length; i++){
                if(args[i] === undefined){
                    args[i] = arguments[arg++]
                }
            }
            return fn.apply(this, args)
        }
    }
    var delay = setTimeout.partial(undefined, 10)
    delay(function(){console.log('delayed 10ms')})

## 5.5 函数重载 （见第4章）


# 第6章 原型及原型链  

    生成原型链，较好的方式： subClass.prototype = new superConstrunctor(); 而不是： subClass.prototype = superClass.prototype;

## HTML DOM 原型， 现代浏览器中，所有dom元素都继承自 HTMLElement 构造函数，可以通过扩展该构造函数原型，来扩展dom 节点的能力

## 判断用户是否按照预期 用构造函数的方式调用了构造函数，而不是作用普通函数调用  

    function User(){
        if(!(this instanceof arguments.callee)){
            return new User()
        }
        ...
        ...
    }