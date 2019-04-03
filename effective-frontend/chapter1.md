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
### 例子：   
* 导航高亮显示：js实现可能出现闪动   
* hover显示menu: 下拉menu 和导航之间的缝隙可以采用伪类 before 填充    
* 自定义radio/checkbox 样式：伪类 :checked 应用   
* 多元素等高： display: table, table-cell    
* 监听回车键提交：利用表单    
* 善于使用css伪类和css3：https://developer.mozilla.org/zh-CN/docs/Web/CSS/:nth-of-type   
* hover 后显示内容：方法1：title， 方法2：属性 data-title 和 伪类 before的应用    

