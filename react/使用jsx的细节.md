# jsx 的使用细节

具体介绍在jsx使用时的细节：主要是DOM元素。

#### 1. 使用 className 代替 class

通过class给html元素添加类名，从而添加样式。不能直接使用class，需要写成 className。

``` html
<!-- 这是错误的 -->
<header class={header}>header!</header> 

<!-- 这才是正确的 -->
<header className={header}>header!</header> 
```

这是因为React中，class用来声明一个组件，而className才是给元素添加类属性的。

#### 2. 使用 htmlFor 代替 for

label 标签的 for 属性，是一个表单元素的id值，用来扩大点击域。要使用 htmlFor 代替 for。

``` html
<input type="text" id="test"/>
<label htmlFor="test">点击</label>
```

这是因为，jsx中for是js的保留字，用来循环了。

#### 3. 事件监听使用小驼峰 onChange

和传统的方式不同，React中，不在通过类似onclick的形式给html5元素注册事件，而是使用小驼峰 --- onClick。

#### 4. 渲染一段 html，而不是直接 text 形式展现

使用属性：dangerouslySetInnerHTML，属性值是个包含__html属性的对象。

**注意：XSS**

``` html
<p
  dangerouslySetInnerHTML={
    {__html: '<a href="www.baidu.com">百度一下</a>'}
  }
></p>
```

#### 5. 用 {/* ... */} 写注释

提倡使用 {/* ... */}，而不是单行注释。
