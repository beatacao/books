# DOM  

    DOM是针对 HTML 和 XML 文档的一个 API. 它描绘了一个层次化的节点结构，允许开发人员增删改查页面的一部分。  
    1998年10月，DOM1级规范成为 W3C推荐标准。   
    注意：IE 中的所有 DOM 对象都由 COM 对象实现，所以，IE中的DOM对象与原生Javascript对象的行为或活动特点并不一致。  

## 10.1 节点层次  

    DOM 可以将任何 HTML 或 XML 描绘成由很多节点组成的有层次的树形结构。每个节点有自己的特性, 数据和方法。各个节点之间的关系构成了层次。  
    文档节点是跟节点（document）, 文档节点只有一个子元素，即文档元素（html）。在HTML中，文档元素就是html元素。在XML中没有预定义的元素，任何元素都有可能成为文档元素。  
    节点有12种类型，它们均继承自一个基类型，即 Node

### 10.1.1 Node 类型  
    
    DOM1 提供了 Node 接口，以类的形式实现。除IE外，其他浏览器都可以直接访问该类。   
    JavaScript 中所有类型节点都继承自Node, 因此都有相同的属性和方法。 每个节点有一个 nodeType 属性（代表该节点类型）。  
    Node 类有12个常量属性，分别表示12个节点类型。   

> 确定节点类型   

    if(someNode.nodeType === Node.ELEMENT_NODE){  //在IE中无效，因为IE无法直接访问Node    
        alert('Node is an element')     
    } 
    if(someNode.nodeType === 1){  //适用于所有浏览器    
        alert('Node is an element')     
    }     

> 节点关系    

    childNodes 字节点，返回一个 NodeList. 每个子元素两个访问方式：childNodes[0], childNodes.item(0)     
    NodeList 是一个类数组，可以通过下标访问。NodeList 是基于DOM 结构动态查询的结果，因此DOM结构的变化能动态反应在NodeList对象中。所以，NodeList是有生命有呼吸的，并不是我们在第一次访问它们时的某个瞬间拍摄下来的一个快照。   

> 节点操作  

    由于关系指针都是只读的（例如 childNodes, parentNode）, 所以DOM提供了一些操作节点的方法：  
    appendChild, insertBefore, replaceChild, removeChild, cloneNode, normalize   
    即使DOM可以看做是一系列指针连接起来的，任何DOM节点也不能同时出现在文档的多个位置。所以节点操作的原节点如果是已经存在的DOM节点，该节点位置会发生移动。  
    replaceChild, removeChild, cloneNode（没添加到文档中之前） 节点仍然属于文档所有，只不过在文档中没有自己的位置。  

### 10.1.2 Document - 12中类型中的其中一种，也是类。基类是Node. 

    . Document 类可以表示 HTML 页面或其他基于XML的文档，不过最常见的应用是 HTMLDocumnent 的实例 document;   
    . document 是 HTMLDocument的实例； HTMLDocument.__proto__ = Document; Document.__proto__ = Node  
    . 有些浏览器下：document.documentElement = document.childNodes[0] = document.firstChild = html元素  
    . document.doctype : 返回 doctype 元素   
    . document.title 可以读也可以写    
    . 与网页请求相关属性： document.URL, document.reference, document.domain(子域之间通信)，所有这些信息都存在于http请求的头部，只不过是通过这些属性让我们能够在js中访问。
    . 查找元素(以下方法同样适用于所有元素查找后代节点）：   
        document.getElementById (IE7及以前版本不区分大小写，并且会查找name 属性)；  
        document.getElementsByTagName : 返回 HTMLCollection(Nodelist), 可以通过数字下标，或name来访问集合中某个元素（namedItem 方法）  
    . 特殊集合： document.anthors (带name 的a链接)，document.links(带href的a链接)，document.images, document.forms  
    . 文档写入：document.write, document.writeln; document.open, document.close; 注意这四个方法在文档加载过程中使用和文档加载完毕使用的区别。    
    . 创建元素：createElement 执行完毕后，会为新元素指定 ownerDocument. 

### 10.1.4 Text   

    document.createTextNode(): 会进行HMTL（或xml，根据当前文档类型）编码。   

### 10.1.5 Comment  

    document.createComment; comment 节点的 data 属性获取注释内容   

### 10.1.6 CDATASection ： xml 文档类型的注释   

### 10.2.3 使用 Nodelist   

    Nodelist , NamedNodeMap, HTMLCollection 都是‘动态的’，即每当文档结构发生变化，它们都会得到更新，并且每次访问都会对文档进行一次查询。    
    死循环实例及解决方法。    
    
    












