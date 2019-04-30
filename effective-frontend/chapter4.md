# HTML5 优化实践

## 使用HTML5的history优化ajax列表，实现前进后退功能  -- 结合vue源码 router的实现（单页面路由）    
* 前进后退功能（history, hash） - demo1
```
    单页面实现前进后退操作，实现方法有两种：
    1、HTML5的history, 兼容性比较差，需要IE10及以上; history.pushState 或 replaceState 会改变ajax的referer
    2、hash, 兼容性好，IE8及以上都可兼容
```

## 使用图标字体代替雪碧图：图标字体原理

## 理解和使用css3动画  - demo2 
* css3是通过关键帧的形式做出来的：首先给动画设定一个时间，然后在时间轴的若干位置插入关键帧，浏览器根据帧的内容做出过渡效果。    
* css 动画主要有两大类：transition 和 animation（关键帧）; 