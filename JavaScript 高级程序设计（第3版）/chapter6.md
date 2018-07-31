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
