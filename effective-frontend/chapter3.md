# 页面优化   - 待细读实践    

## 避免页面卡顿    
* 拆分代码段：window.requestAnimationFrame    
* 减少layout：使用性能较高的样式（参考：csstriggers）   
* 简化DOM，尤其是scroll或者需要动画的时候    

## 加快页面打开速度   
* 页面打开速度查看指标：ready时间，load时间，chrome devtools中 network 标签状态栏查看
    1、ready时间（DOMContentLoaded）：DOM树解析完整，页面可交互状态   
    2、load时间（load）：页面资源加载完毕   
### 加快页面打开速度的几种方法    
#### 一、避免渲染阻塞    
* 避免head标签JS阻塞： head 里面的js 和 css都会堵塞dom的解析和渲染   
* 减少head标签里面的css：css需要放到head标签，因为如果放到body底部，待css加载完毕，会造成页面的重绘，可能出现闪烁；思路是尽量减小css的体积： 
    1、尽量避免在css中使用base64图片（css体积会变大，并且失去动态加载图片资源的优势）
```
    关于hover时动态加载图片的需求，hover时需要变换图标的颜色，几种解决方法：
    1、将正常状态和hover状态的图片都转换为base64, 写到css文件：缺陷是css体积变大，如果hover效果没用到，会有多余加载    
    2、图标为svg, 在svg控制颜色变换：缺陷是如果配合图标的还有文字，文字颜色变换不能放到svg; svg有跨域的问题     
    3、使用字体图标（推荐）
```    
    2、如果css体积不会过于大，可以考虑把css写成内联css( 省去解析DNS，建立连接等的时间，对于缓存不利，利于首次加载；具体是否合适，根据开发者工具各项消耗时间具体指标决定)   
#### 二、图片优化   
* 使用响应式图片   
* 懒加载   
#### 三、压缩和缓存    
* gzip    
* 浏览器缓存   
#### 四、升级到HTTP2    
* 只需建立一个http连接，通过多路复用实现多个资源并行加载    
* 报文头压缩，使用二进制传输
* server push: 无需等待html加载解析完毕才可以加载其他资源    
#### 五、其他优化方法   
* dns预解析：需要加载多个外部域名的资源时，<link rel='dns-prefetch' src='http://www.xxx.com'/> ； 由于它是并行的，不会阻塞页面渲染     
* html优化：压缩，去除注释，空格等减少体积     
* 代码优化：如html嵌套不要太多，减少浏览器layout的消耗，css使用高性能的属性，js不要滥用全局变量和闭包，避免作用域链太深增加查找时间等   

## 增强用户体验   


# 延伸学习资料    
* https://developers.google.com/web/fundamentals/  
* 使用更高性能的css：
    1、https://csstriggers.com/  
    
* 页面生命周期： 
    1、https://github.com/fi3ework/blog/issues/3   
    2、http://zhouchen.tech/2018/11/17/html%E9%A1%B5%E9%9D%A2%E7%9A%84%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%EF%BC%9A%E4%BB%8E%E5%87%BA%E7%94%9F%E5%88%B0%E6%88%90%E9%95%BF/