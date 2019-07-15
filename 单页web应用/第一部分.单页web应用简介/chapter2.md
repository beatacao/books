# 温故Javascript
* 类型宽松：定义变量时无需声明类型
* 动态：随时可以修改变量的赋值

* 变量声明语块 + 对象字面量
* 变量提升（声明被提升，初始化没有）：js的变量声明会被提升到函数顶部，而初始化并没有提升，还是在原来的地方

## 高级变量提升和执行环境对象
* 为什么会有变量提升
```
js 在进入作用域的时候，会对代码进行两轮处理：
1、初始化变量：声明并初始化参数、声明变量但不初始化，声明并初始化函数定义
    因为进入作用域时，参数的值都是已知的，所以会初始化；而变量需要到执行时才可以得到值，因此无法初始化；函数定义也可以初始化
2、执行代码：执行环境 -> 执行环境嵌套
var a = 1;
function foo(a){
    console.log(a)    // 输出1，因为进入作用域会声明并初始化参数，这时 a是已经定义的变量
    var a;  // 无效的定义
}
```
* 作用域链：函数作用域是通过词法来划分的，因此作用域链是在函数定义的时候就固定了的。
```
function foo(){
    var a = 1;
    bar()   // 会报错， a undefined
}
function bar{
    console.log(a)
}
```

## 原型和原型链

### 原型
```
实例化的两种方法：new 和 Object.create
作者推荐使用 Object.create, 原因是因为 new 是类的用法，而js上的原型本质上不算类，这样使用容易引起熟悉类的开发人员的误解。
Object.create 对 IE8 及其一下版本是不支持的，需要做兼容：
var objectCreate = function(arg){
    if(!arg) return {}

    // 正确写法
    function obj(){}
    obj.prototype = arg
    return new obj()

    // 错误写法, 这种写法会导致查找原型链失败，因为原型链的查找是查找 __proto__， 不是 prototype
    var obj = {}
    obj.prototype = arg
    return obj
}
Object.create = Object.create || objectCreate


两者低层运作应该是一样的：
1、prototype

function foo(a, b){
    this.a = a
    this.b = b
}
foo.prototype = {
    method1: fn,
    prototype1: 'pt1'
}
var f1 = new foo('a', 'b')

2、Object.create
var proto = {
    method1: fn,
    prototype1: 'pt1'
}
function makeFoo(a, b){
    var obj = Object.create(proto)
    obj.a = a
    obj.b = b
    return obj
}
var f1 = makeFoo('a', 'b')

```

### 原型链
* 原型链的查找，搜索的是 __proto__ 属性
* 通过 new 生成的实例，构造函数的 prototype 会转化为实例内部属性 __proto__

## 函数
* 自执行匿名函数
* 模块模式 - 私有变量
* 闭包
