# 面向对象的程序设计  

    ECMA-262 对象定义： 无序属性的集合，属性值可以是基本类型，函数或对象。因此可以把js中的对象看成是散列表。

## 6.1 理解对象  

    无论是通过原生构造函数创建还是字面量直接定义，对象的属性在创建时都会带有一些特征值，JavaScript通过这些特征值来定义它们的行为。  

### 6.1.1 属性类型（数据属性和访问器属性）  

    ECMA-262 第5版在定义只有在内部才用的特性时，描述了属性的各种特征。ECMA-262定义这些特性是为了实现JavaScript引擎用的，因此在 JavaScript 中不能直接访问它们。为了表示特性是内部值，该规范把它们放在了两对方括号中，例如：[[Enumerable]]  

#### 数据属性  
. 四个描述数据属性的特性： [[Configurable]], [[Enumerable]], [[Writalbe]] (这三个默认为true), [[Value]] (默认 Undefined)  
. 要修改属性默认的特性，必须使用 Object.defineProperty() 方法
. 使用 Object.defineProperty 方法定义的属性，如果没有设置，[[Configurable]], [[Enumerable]], [[Writalbe]] 默认均为 false  
. 把 configurable 设置为false 后， 就不能再修改为可配置了，此时通过 Object.defineProperty 修改除 writalble 之外的特性，都会导致错误。  

    ps: IE8 是第一个实现Object.defineProperty 方法的浏览器版本。然而这个版本的实现存在诸多限制，比如：只能在DOM对象上使用这个方法，而且只能创建访问起属性。由于实现不彻底，建议不在IE8中使用  

#### 访问器属性  
. 四个描述访问器属性的特性：[[Configurable]], [[Enumerable]] （默认true）, [[Get]], [[Set]] (默认 Undefined)  

    在早起浏览器版本中，没有 setter 和 getter方法，可以通过两个非标准方法来定义访问器属性：__defineGetter__, __defineSetter. 
    不支持 Object.defineProperty 方法的浏览器中，不能修改 [[Configurable]], [[Enumerable]]  

### 6.1.2 一次定义多个属性 Object.defineProperties (IE8及以下不支持)  
### 6.1.3 读取属性特性 Object.getOwnPropertyDescriptor(obj, xxx)  

> 通过该方法，可以得知，对于通过字面量定义的对象，无论属性是基本类型，函数还是对象，属性均为数据属性。  

## 6.2 创建对象  

. Object ， 字面量：缺陷，大量重复代码  
. 工厂模式： 缺陷，创建的对象没有类型   
. 构造函数： 优点，有类型（instanceof）; 缺点，需要为每个实例创建方法，各个实例之间方法并不相等  
. 原型模式  
. 组合使用原型模式和构造函数模式  
. 动态原型模式  
. 寄生构造函数模式  
. 稳妥构造函数模式  

### 6.2.3  

    我们创建的每个函数，都有一个prototype属性，该属性是一个指向函数原型对象的指针。原型对象的用途是包含由某中特定类型的对象所共享的属性和方法。  

#### 理解原型对象  

. 创建一个函数时，默认的原型对象会自动包含一个 constructor 属性，该属性是一个指针，指向原型对象所在函数，即构造函数。至于原型对象中的其他方法，都是从Object继承而来的。  
. 构造函数的每个实例，有一个内部属性[[prototype]]（某些浏览器环境中，可以通过 __proto__ 来访问），改属性是一个指针，指向构造函数的原型对象。注意：从某种程度上讲，实例和构造函数没有直接关系，实例的 __proto__ 指向的是构造函数的原型对象。  
. 实例的同名属性会覆盖原型对象的属性，如需继续访问原型属性，可通过 delete 删除实例属性

    Person.prototype.isPrototypeOf(person)  //true  
    Object.getPrototypeOf(person) === Person.prototype  //true  Object.getPrototypeOf IE8及一下不支持  
    getOwnPropertyDescriptor 只能获取实例自身属性特性，如需获取原型属性特性，将该方法应用到原型对象  

#### 原型 与 in操作符  

. 只要属性能访问到（无论在实例中还是原型中）均返回true  
. !person.hasOwnproperty(xxx) && (xxx in person)  判断 xxx 是原型属性  
. for in : 遍历所有可枚举属性（Enumerable 为true）, 无论是实例还是原型对象中的属性  
. 只获取实例属性：Object.keys (可枚举属性)， Object.getOwnPropertyNames (所有属性key)  
. 更简单的原型语法：   

    function Person(){}   
    // 第一种方法
    Person.prototype = {   // 直接重新原型对象，会导致无法正确使用 constructor判断实例类型  
        name: 'aaa',   
        sayName: function(){}   
    }  
    // 第二种方法 
    Person.prototype = {   // 这种方式使得 constructor 成为可遍历，原型对象自动获得的constructor是不可遍历的 
        constructor: Person
        name: 'aaa',   
        sayName: function(){}   
    }  
    // 第三种方法  
    Person.prototype = {    
        name: 'aaa',   
        sayName: function(){}   
    }  
    Object.defineProperty(Person.prototype, 'constructor', {
        value: Person,
        enumerable: false
    })  
    
. 原型的动态性：可以随时修改原型的方法和属性，并及时反应到原型的所有实例上，这归结于实例和原型之间的松散连接关系。但是不可以重写原型对象，会切断现有实例和当前原型的联系，因为现有实例原型仍指向重写前原型对象。

    该书认为：原型模式，即把所有属性和方法定义到prototype的方式。而在构造函数定义特殊属性，共用属性定义在prototype的方式为构造函数模式和原型模式组合使用  

### 6.2.6 寄生构造函数模式  
    该模式可以用于为对象创建特殊的构造函数。例如：不修改原生对象原型的情况下，生成某些原生对象实例，这些实例拥有对原生对象的扩展，如下：  
    function SpecailArray(){  
        var values = new Array()   
        values.push.apply(values, arguments)    
        values.toPipedString = function(){  
            return this.join('|')  
        }  
        return values  
    }  
    var colors = new SpecialArray('red', 'yellow', 'blue')   
    colors.toPipedString()  

    > 通过寄生构造函数创建的对象，与寄生构造函数与其原型都没有关系。因此使用 instanceof 操作符无法判断。  
### 6.2.7 稳妥构造函数模式  
    稳妥对象：没有公共属性，而且其方法也不引用this. 适合在安全环境（禁止使用this和new）下的代码。  
    稳妥构造函数（安全性）和寄生构造函数一样（不过只能通过其定义的方法访问属性，不能直接访问传入的原始数据），不过创建对象时，不适用new操作符。其创建的对象同样和构造函数及原型没有关系，instanceof 也无意义。  

    function Person(name){  
        var person = new Object()
        person.sayName = function(){
            console.log(name)
        }
        return person
    }  
    var p1= Person('xiaoming')  //name属性只能通过方法sayName访问，不能直接访问原始输入  

## 6.3 继承  

    面向对象继承包括两种方式：接口继承（只继承签名）和实现继承（继承实际的方法）；由于函数没有签名，所以ECMAScript只支持实现继承，无法实现接口继承，而其实现继承主要依靠原型链。  

JavaScript 中的继承主要通过原型链实现。  

继承笔记 ----- 待详细






