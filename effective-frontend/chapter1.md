# HTML/CSS 优化
## 前言：切图三境界 
1、精准：还原设计稿    
2、灵活：考虑到动态内容的复杂多样性，使得页面具有响应式，自适应等特点    
3、良好交互和体验：如能否自动监听用户回车提交等    

## 原则1：能使用 HTML/CSS 解决的就不要使用 JS    
```
    支撑该原则的理论基础：HTML，CSS是浏览器提供的功能，原生功能性能和效率大概率是比较好的。        
    使用HTML/CSS开发，只需几个简单的标签和样式即可解决问题，代码简单，易于维护，开发效率高。   
    JS实现，有可能碍于JS加载和执行所需时间，会造成最终效果出现闪动等不良体验。     
```
### 例子：（部分例子实践见 ./chapter1/demo1.html）
* 导航高亮显示：js实现可能出现闪动   
* hover显示menu: 下拉menu 和导航之间的缝隙可以采用伪类 before 填充    
* 自定义radio/checkbox 样式：伪类 :checked 应用   
* 多元素等高： display: table, table-cell    
* 监听回车键提交：利用表单    
* 善于使用css伪类和css3：https://developer.mozilla.org/zh-CN/docs/Web/CSS/:nth-of-type   
* hover 后显示内容：方法1：title， 方法2：属性 data-title 和 伪类 before的应用    

## 原则2：使用HTML语义化标签    
* HTML5新增标签   

## 技巧： 使用 css 实现各形状的三角形：底层知识点（border, position）   

## 原则3：伪元素的使用    
### 什么是伪元素
* 是一个元素的子元素，意味着img,input等不能包含子元素的标签，使用伪元素时会被浏览器忽略   
* 默认时一个inline元素，对伪元素使用定位样式后，会编程块元素   
* 不是一个真实的元素，因此不能通过JS查询，增、删、改，对JS是透明的。因此不会增加JS查询DOM 的负担，对SEO也是有好处的。   

### 伪元素使用场景：作为辅助元素，比如边框、样式等小元素或对某些元素的辅助说明    

### 应用案例 (部分例子实践见 ./chapter1/demo2.html)   
* 清除浮动    
* form 表单的编辑和只读状态   
* 选择框计数器    
* 小游戏   


# 延伸课题研究    
* css 伪类，css3，可用css 而非js实现的各种效果     
* HTML5标签的应用    
* 伪元素及伪元素的应用   

# 参考    
* https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS3     
* google fonts: https://developers.google.com/fonts/docs/getting_started   