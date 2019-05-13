# DOM 扩展

    DOM 是一种 API， 尽管已经非常完善了，但是为了实现更多操作，还是出现了一些扩展。      
    这些扩展大多来自开发社区，2008年之前，几乎所有DOM扩展都是专有的。 DOM 将一些已经成为事实标准的扩展标准化，并写入规范。     
    主要扩展包括：selectors api(选择符)， html5 和 element traversal(元素遍历)    

## selectors api (w3c 发起制定的一个标准)   

    在浏览器底层对dom的查询，有些返回的是元素，有些返回的是节点（node, nodelist）; 从行为上，有些是不断查询的动态操作（会涉及到性能问题）     
    . querySelector: 返回一个元素   
    . querySelectorAll: 返回一个节点数组（nodelist）, 相当于快照。不是通过动态查询，不涉及性能问题。   
    . matchesSelector   

## 元素遍历规范（element traversal）   

    以下几个新定义的方法，主要为了解决ie9之前版本和其他浏览器行为不一致的兼容性问题：对于元素之间的空格，ie9之前的版本不会返回文本节点，而其他浏览器都会返回文本节点，这一差别会导致在使用childNodes, firstChild等属性时行为不一致。所以添加以下方法：   
    . childElementCount, firstElementChild, lastElementChild, previousElementSibling, nextElementSibling


