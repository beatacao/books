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

### 柯里化函数

## 防篡改对象
```
    对Javascript库的开发者来说，保证核心功能不被有意或无意的篡改，是很重要的。
    而js共享的本质，使得在同一环境下运行的代码可以任意修改对象。
    ECMAScript5 致力于解决这个问题，让开发人员可以自定义防篡改对象。
```
### 一级防篡改（preventExtensions）
* Object.preventExtensios(obj): obj不能扩展属性和方法（非严格模式静默失败，严格模式报错），可以修改属性和方法的赋值
* Object.isExtensible(obj) 判断

### 二级防篡改（seal）
* Object.seal(obj): 不能扩展；不能修改数据属性为访问器属性，反之也不行。可以修改属性和方法的赋值。
* Object.isSealed(obj)

### 三级防篡改（freeze）
* Object.freeze(obj): 不能扩展，不能在数据属性和访问器属性之间改变，不能修改属性值；如果设置了[[set]]，还是可以通过访问器属性修改属性值。
* Object.isForzen(obj)

## 高级定时器

### 重复定时器
* setInterval 存在的问题：1、某些间隔会被忽略跳过（并不会添加到队列）；2、多个定时器代码执行间隔可能小于设定的时间    
* 解决以上两个问题，设定重复定时器： setTimeout 嵌套调用   
* 每个浏览器窗口，标签页和frame都有自己独立的执行队列，进行跨域定时调用时，如果代码同时执行可能导致竞争条件。因此跨域定时调用，最好在接收窗口或frame建立一个定时器来执行代码。   
 
## Yeilding Processes  
```
    不同于桌面应用（往往能够随意控制代码运行所需的内存和时间），运行在浏览器中的js只被分配了有限数量的资源，运行受到严格的限制。
    其中一个限制是长时间运行的脚本，如果运行时间超过限定时长或超过限定语句数量，就不允许默认继续执行。
```
* 数组分块（array chunking）
* 函数节流（throttle）

## 自定义事件
* 事件是一种观察者设计模式，可以创建松耦合代码。    
* 拖放（鼠标拖尾）



# 扩展参考资料
* https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof
* 安全类型检测：https://flycode.co/archives/241735
* https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/instanceof
* https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind