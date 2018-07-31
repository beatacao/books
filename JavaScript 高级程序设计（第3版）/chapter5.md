# 引用类型
引用类型的值（对象）是引用类型的一个实例。ECMAScript 中，引用类型是一种数据结构，为了把数据和功能组织在一起，它也常被称为类。尽管ECMAScript从技术上讲是面向对象编程的语言，但它不具备传统面向对象语言的类和接口等基本结构。引用类型也被成为对象定义，因为它描述的是一类对象所具有的属性和方法。
虽然类和引用类型很相似，但它们不是相同的概念。

## 5.1 对象定义
1. new Object
2. 字面量定义，为了简化创建包含大量属性的对象定义。使用改方法定义对象时，并没有调用Object构造函数。
3. 定义空对象，即是定义了一个只包含默认属性和方法的对象
4. 对象属性如果为数值类型，会自动转化为字符串
5. 对象属性访问方式：点访问，方括号；其中方括号访问支持变量或非法字符（比如空格）

ps: 
1. 新概念 - 语句上下文，表达式上下文
2. 传递参数：用命名参数定义必传参数，多个选传参数可以用对象形式

## 5.2 数组
1. 通过改变数组length属性的值，可以实现对数组元素的增删
2. 类型检测：instanceof (多个全局执行环境下检测会有问题)，Array.isArray, Object.prototype.toString.call
3. 转换方法：每个对象均有toLocaleString, toString, valueOf 方法；数组的 toLocaleString 和 toString 方法是通过调用数组中每一项的toLocaleString 和 toString 方法得到每一项的字符串表示，再通过逗号连接起来的字符串；数组的valueOf 返回的仍是数组。ps: alert接收字符串作为参数，所以alert(arr)会弹出arr的字符串表示
4. 栈、队列、反向队列方法：push，pop, shift, unshift 方法的组合，可以模拟栈（push, pop），队列(push, shift)，反向队列(unshift, pop)
5. 重排序方法：reverse, sort; reverse只是简单反转了数组元素的顺序； sort默认是对数组中每个元素的字符串表示进行比较（对每项元素调用toString字符串化后进行比较，因此默认情况下对数值类型数组排序并不是我们想要的），可以接受一个回调函数来自定义排序逻辑；PS: 由于ECMAScript 标准并没有对sort中使用什么算法做明确规定，因此各个浏览器都有自己的实现算法，算法的时间复杂度和运行时间也会有差异。
6. 操作方法：  
    concat(复制原始数组，并将参数种的每一项添加到复制数组末尾，返回新数组)  
    slice(从原始数组复制元素，生成新数组，如果是两个参数，不包含第二个参数所在位置元素)  
    splice(会修改原始数组，可以删除，添加袁数组元素，返回包含被删除元素的数组，如果没有元素被删除，返回空数组)
7. 位置查找：indexOf, lastIndexOf, 第二个参数表示查找起始位置索引，不是必传；比较操作使用的是全等运算符，如下：  
    var person = {name: 'aaa'}  
    var arr = [{name: 'aaa'}]  
    var arr2 = [person]  
    arr.indexOf(person) //-1  
    arr2.indexOf(person) //0  
8. 迭代方法，所有迭代方法都不会修改原数组；所有迭代方法接受两个参数，第一个是函数类型，该函数接受三个参数（数组元素值，数组元素索引，数组）；第二参数不是必须的，表示运行第一个参数函数是的作用域；  
    every,some: 返回逻辑值  
    filter, map：返回新生成的数组  
    forEach: 没有返回值  
9. 归并方法：ECMAScript5 添加的新方法，reduce, reduceRight; 不会修改原数组，返回对数组种每个元素执行某种归并操作后的运算值；

## 5.3 Date对象 --- 待细读

## 5.4 RegExp --- 待细读

## 5.5 Function

1. 函数是对象（Function的实例），函数名是指向函数对象的指针  
2. 三种定义方式：函数声明，函数表达式，Function构造函数（不推荐，因为引擎需要解析两次，有性能问题）  
    function sum(a,b){
        return a+b;
    }
    var anotherSum = sum
    sum(10, 10) //20
    sum = null
    anotherSum(10, 10) //20, 虽然sum已经被重置为null, anotherSum仍能顺利执行，说明函数名是指针  
3. 函数声明和函数表达式区别：函数声明提升和普通变量提升的区别  
4. 函数内部两个对象：arguments, this  
    arguments: 类数组，包含传入函数的所有参数，主要作用是保存参数。该对象有个 callee 属性，该属性为一个指针，指向拥有该arguments对象的函数。callee 属性一般用于解除递归调用中对自身函数名的耦合。
    this: 函数据以执行的环境对象
    caller: ECMAScript5新添加。函数对象属性，该属性保存着当前函数的调用者的引用。也可通过arguments.callee.caller 来访问。arguments.caller 始终返回undefined; 在严格模式下 arguments.callee 和 argument.caller 都是不可用的；  
    ps: 非严格模式下，定义arguments.caller 是出于安全考虑，区分 caller 和 arguments.caller，这样第三方代码在相同的执行环境下， 就不能窥视其他代码了。  
5. 函数的属性和方法：函数为对象，它也有属性和方法  
    属性：length(函数期望传入的命名参数的个数)， prototype  
    方法：apply, call, bind(这三个方法均非继承而来)；ps: 严格模式下，全局调用函数，并不会把this默认指向window, 而是指向 undefined
    继承而来的方法：toString, toLocaleString, 这两个方法均会返回函数源代码，在不同浏览器下会有所不同，有的会返回函数代码的内部表示（即解析器解析过后的代码），对调试有帮助。

## 5.6 基本包装类型

1. 读取基本类型时，js内部进行的隐式包装类型创建和销毁  
2. 基本类型，通过new 构造函数和不带 new关键字的构造函数创建时，区别  
    var a = new Object(12)  
    var b = new Number(10)
    var c = Number(5)  
    typeof a    //object
    typeof b    //object
    typeof c    //number
    a instanceof Object //true
    a instanceof Number //true  
3. Number 的几种方法：toFixed, toExponential, toPrecision, 这三种方法均可以指定最后保留几位数，并且均由自动舍入功能
4. String: 访问字符串种每个字符，charAt, charCodeAt, 方括号;  
    字符串截取：substr, substring, slice, 均不改变原字符串，参数为负数时，substr(第一个参数为负数，转化为length-n, 第二个参数为负数，转换为0)； substring(所有参数为负数时，统一转换为0)； slice(所有参数为负数时，统一转换为length-n)
    字符位置：indexOf, lastIndexOf
    ECMAScript5新增方法：trim, trimLeft, trimRight, 这三个方法会创建原字符串的副本并去除头尾空格，原字符串不会改变；
    大小写转换：toLowerCase, toUpperCase, toLocaleLowerCase, toLocaleUpperCase, 一般情况，针对地区的方法和通用方法返回的值是相同的，但是，某些特殊语言（如土耳其语）会对unicode大小写转换应用特殊的规则，因此，在不确定自己的代码在何种语言环境运行的时候，最好使用针对地区的方法  
    > *字符串的模式匹配方法：match, search, replace , split --- 待细读+实践*  
    字符串比较：localeCompare       
    String构造函数本身还有一个静态方法：fromCharCode: String.fromCharCode(104,101) //'he'  
    HTML方法：不建议使用,如：var txt = 'text'; txt.anchor('name'); 会生成字符串："<a name='name'>text</a>" 

## 5.7 单体内置对象 

1. 内置对象：由ECMAScript实现提供，不依赖宿主环境的对象，这些对象在ECMAScript程序执行之前就已经存在。开发人员不必显示的实例化内置对象。内置对象包括：Array, Object, String等。ECMA-262还定义了两个单体内置对象：Math 和 Global  
2. Global对象：ECMAScript中的Global对象，在某种程度上充当了‘兜底对象’的角色，即当属性或方法不属于任何其他对象时，就属于Global对象。在web浏览器中，是将该对象作为window对象的一部分加以实现的。    
    #### 2.1. URI编码方法：encodeURI, encodeURIComponent；  

    > 参考：  
    > http://www.ruanyifeng.com/blog/2010/02/url_encoding.html  
    > https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/encodeURI  

    #### 2.2 eval  

    . 像是一个完整的ECMAScript解析器，接收一个ECMASCript(或javascript)字符串作为参数。  
    . 参数不是字符串时，将原封不动返回参数  
    . 当解析器遇到eval时，会将其参数作为ECMAScript语句来解析，并将执行结果插入到原位置。  
    . 通过eval执行的代码，被认为是包含本次调用的执行环境的一部分，因此与该执行环境有着相同的作用域链。即：eval可以访问该执行环境外部变量和函数，eval中定义的变量和函数，也可以被其后执行的代码调用。  
    . eval中的代码没有变量提升，只有在执行时才被创建。  
    . 间接调用eval时，其所在作用域为全局作用域，如下： 

        function test() {  
            var x = 2, y = 4;  
            console.log(eval("x + y"));  // 直接调用，使用本地作用域，结果是 6  
            var geval = eval; // 等价于在全局作用域调用  
            console.log(geval("x + y")); // 间接调用，使用全局作用域，throws ReferenceError 因为`x`未定义  
            (0, eval)('x + y'); // 另一间接调用的例子  
        ​}  
    
    . 严格模式下，在外部访问不到eval中定义的任何变量和方法。给eval赋值也会报错。  
    . 应尽量避免使用eval（易读性差，不能提前编译和进行优化，因此相对于替代方法，一般会比较慢，存在安全隐患，压缩混淆有时会报错）
    . 安全：注意代码注入。 eval中执行的代码会看到外部执行环境。  
    . 引申问题：javascript 为什么不推荐用 eval ?
3. Math 对象：保存数学公式和信息

