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

### 表单字段   

#### 表单字段是什么   
* 表单字段对应的是DOM中form表单下的表单元素，如：input, textarea, button, fieldset，select等；普通元素不算（比如：li, div等）   

#### 表单元素获取方式   
* form 属性：form[0], 不推荐使用这种方式，该方式是为了向后兼容低版本浏览器而保留的
* form.elements[name]:  如果多个表单元素使用同一个name，该访问方式返回一个 Nodelist, 可以通过 form.elements[name][index] 来访问某一元素
* form.elements[index]

#### 不同的表单元素之间共同有的字段属性   
* 除了 fieldset 元素之外，所有表单元素都有共同的属性，input元素根据type属性的不同可以表示多种元素，有些属性只适用于特定的元素
```
disabled: 代表该元素是否被禁用
type：元素类型，可以修改，但不建议修改
name
value：提交到服务器端的值，可以修改；file 类型的该属性为只读，包含了文件在计算机的路径
form: 指向该元素所在表单的指针，只读
tabIndex: 当前元素切换（tab）的序号
readOnly: 表示元素是否只读
```

* 关于表单重复提交的问题（仅针对使用 submit按钮提交来说）
```
在 form 的submit 时间中将 submit 按钮设置为 disabled 状态；
不要在 submit 按钮的 click 事件中禁用，因为不同浏览器存在‘时间差’： 有些浏览器是在执行 click 时间之后才执行submit的（这种情况下，click 中禁用按钮，submit将永远不会执行），而另外一些浏览器则相反。
```

* form 元素type值, select元素的type是只读的
```
除了 fieldset 元素外，所有表单元素都有type值：
1. input 和自定义 button 的type 值为元素 type 属性的值
2. select type 值为 'select-one'
3. select multiple 的type值为 'select-multiple'
4. button 默认type值为 submit
```

#### 不同的表单元素共有的方法  
* focus: 将浏览器的焦点设置到某个表单元素，激活该元素，使其可以接收键盘输入; 另外还有 autofocus 属性，在支持的浏览器中可以达到同样的效果  
* blur: 在表单元素还没有readOnly 属性时，常用来实现只读效果

#### 不同表单元素共有的事件
* blur
* focus
* change: input 和 textarea 在value改变，并且失去焦点，才会触发 change 事件；select 在用户选择改变后就触发 change事件   
* 注意：不能总是假设 blur 事件发生在 change 事件之前或之后，这两个事件的发生顺序在各个浏览器下是不同的。

## 文本框脚本
* <input type='text' maxlength='50' size='25' value='init value'/>
* <textarea rows='5' cols='100'>init value</textarea>
* select() 方法和 select 事件
* 过滤输入：阻止keypress 事件的默认行为
* 剪切板操作
* 自动切换焦点（提升用户体验，需要知道每个输入框的最大输入长度，响应keyup事件）
* HTML5 验证：required; type:url, type:email, type:number(min,max,step); stepUp(num), stepDown(num); pattern

## 表单序列化
* 提交表单时，数据默认是序列化的 encodeURIComponent
* select 选中的项的传参默认传 value 如果没有，传递 text

## 富文本编辑
* designMode
* contenteditable
* document.execCommand