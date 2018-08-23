# DOM  

    DOM是针对 HTML 和 XML 文档的一个 API. 它描绘了一个层次化的节点结构，允许开发人员增删改查页面的一部分。  
    1998年10月，DOM1级规范成为 W3C推荐标准。   
    注意：IE 中的所有 DOM 对象都由 COM 对象实现，所以，IE中的DOM对象与原生Javascript对象的行为或活动特点并不一致。  

## 10.1 节点层次  

    DOM 可以将任何 HTML 或 XML 描绘成由很多节点组成的有层次的树形结构。每个节点有自己的特性, 数据和方法。各个节点之间的关系构成了层次。  
    文档节点是跟节点（document）, 文档节点只有一个子元素，即文档元素（html）。在HTML中，文档元素就是html元素。在XML中没有预定义的元素，任何元素都有可能成为文档元素。  
    节点有12种类型，它们均继承自一个基类型。  

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


