# 表单脚本   
```
    在html中，用<form>来表示表单，在js中，表单对应的则是 HTMLFormElement类型，该类型继承了HTMLElement类型。
```

## 表单基础知识   
### 获取表单元素
* document.getElementById()
* document.forms[index], document.forms.formname
* document.formname -- 不推荐，容易出错并将来浏览器可能不支持   

### 表单提交   
* 点击三类按钮（浏览器在发送请求给服务器之前会触发表单的submit事件，便于验证表单，阻止表单提交等控制操作）
    1、 input:submit  
    2、 button:submit
    3、 input:image
* js触发：form.submit()，浏览器发送请求到服务器，不会触发submit事件，因此需要在调用该方法之前做好验证   
* 表单提交注意事项：避免重复提交  

### 重置表单    
* 通过 type='reset' 按钮 或 form.reset() 方法都可以重置表单为页面刚加载完毕时的状态   
* 注意区分重置和清空， reset 方法为重置表单到页面加载完毕时的初始值    
* reset 对隐藏域不起作用    
