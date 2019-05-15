# 高级技巧
```
    Javascript 语言天生的动态属性，使得其有很多强大和有趣的使用模式，最常用的有面向对象和面向过程。
    这些模式利用ECMAScript语言的特性，结合BOM扩展和DOM功能产生强大的效果。
```

## 高级函数
```
    js中函数皆对象，所以使用函数指针非常方便。
    js中使用函数可以是非常简单和过程化的，也可以是很复杂和动态的。
    本节介绍几个js中使用函数的高级方法
```
### 安全的类型检测  
* typeof (不准确): 返回 undefined, number, string, boolean, function, object; 不能区分null, array, 正则和对象
* instanceof (不准确)
    1. obj instanceof Array, 用户测试 Array.prototype 是否出现在 obj 原型链的任意位置    
    2. 并不总是返回true 或 false, Array.prototype 可能会被改变，obj 的原型链也可能被改变(obj.__proto__)
    3. 在多个全局作用域（多个iframe或多个window对象之间）下有问题，毕竟 Array 是window对象的属性
* constructor: Null 和 Undefined 被浏览器保护，不允许外部访问
* Object.prototype.toString.call：（推荐）该方法返回一个字符串[object NativeConstructorName]。每个类在内部都有一个[[Class]]属性指向原生构造函数名。由于原生对象的构造函数名与全局作用域无关，因此该方法能保证返回的值一致。
* 注意：toString 方法对于低版本IE浏览器不适用（使用COM对象）；另外 toString 方法也可能会被修改。
```
    总结：
    1、typeof 返回被检测数据的类型标签，null 的类型标签为object
    2、instanceof(constructor同理)检查的是对象的原型链（因此需要同一个全局作用域）
    3、toString 方法返回对象原生类的构造函数名
```

### 作用域安全的构造函数 及 构造函数窃取
* 限定构造函数的执行环境，避免不经意之间污染全局变量，导致意外

### 惰性载入函数
* 对于if分支判断，只执行一次

### 绑定函数
* 绑定函数主要是为了为函数执行指定特定的this上下文
* ECMAScript5 为所有函数定义了原生的bind方法，简化了绑定操作（ie9+ 支持）

```
    // 手动实现
    function bind(fn, context){
        return function(){
            return fn.apply(context, arguments)
        }
    }
    // Function.prototype.bind polyfill

    // 特殊应用 - 实现函数的简短定义   
    var slice = Array.prototype.slice
    slice.apply(arguments)

    var sliceshort = Function.prototype.apply.bind(slice)
    sliceshort(arguments)
```

# 扩展参考资料
* https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof
* 安全类型检测：https://flycode.co/archives/241735
* https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/instanceof
* https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind