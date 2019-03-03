# 深度理解jsx

为了更简洁地描述UI，我们更倾向于直接写jsx，不再写react的原生createElement方法。

jsx为 `React.createElement(component, props, ...children)`提供语法糖。

``` js
<MyButton color="blue" shadowSize={2}>
  Click Me
</MyButton>

=> 

React.createElement(
  MyButton,
  {
    color: 'blue',
    shadowSize: 2
  },
  'Click Me'
)



// 对于自闭和的元素，也同样编译转化

<div className="sidebar" />

=> 

React.createElement(
  'div',
  { className: 'sidebar' },
  null
)
```

[这儿](https://babeljs.io/repl/#?presets=react&code_lz=GYVwdgxgLglg9mABACwKYBt1wBQEpEDeAUIogE6pQhlIA8AJjAG4B8AEhlogO5xnr0AhLQD0jVgG4iAXyJA)是在线编译工具。

## 指定React元素类型

jsx标签的第一部分确定了React元素类型。

除了传统的h5标签外，大写的标签是指这个jsx标签是个React组件。

如果一个React模块内导出多个React组件，可以使用 **.** 来使用某一组件。

``` js
import React from 'react';

const MyComponents = {
  DatePicker: function DatePicker(props) {
    return <div>Imagine a {props.color} datepicker here.</div>;
  }
}

function BlueDatePicker() {
  return <MyComponents.DatePicker color="blue" />;
}
```

**另外**：

- 组件名必须大写，会递归调用React.createElement。
- 标签不能是表达式。
  ``` js
    import React from 'react';
    import { PhotoStory, VideoStory } from './stories';

    const components = {
      photo: PhotoStory,
      video: VideoStory
    };

    function Story(props) {

      // 不能使用components[props.storyType]直接替换SpecificStory
      const SpecificStory = components[props.storyType];
      return <SpecificStory story={props.story} />;
    }

  ```

## 在jsx中的props

有以下方式表示属性prop：

#### 默认是true

``` js
<MyTextBox autocomplete />

等同于

<MyTextBox autocomplete={true} />
```

#### js表达式

``` js
// 一元或者三元表达式
<MyComponent foo={1 + 2 + 3 + 4} />

// 不能使用if/for，但是可以先计算出来
function NumberDescriber(props) {
  let description;
  if (props.number % 2 == 0) {
    description = <strong>even</strong>;
  } else {
    description = <i>odd</i>;
  }
  return <div>{props.number} is an {description} number</div>;
}
```

#### 字符串

直接使用字符串，可不用加{}，可直接用符号代替实体。

``` js
<MyComponent message="&lt;3" />

<MyComponent message={'<3'} />

```

#### 扩展运算符

用来传递多个属性。但是如果很容易将不必要的属性传递过去。

``` js
function App1() {
  return <Greeting firstName="Ben" lastName="Hector" />;
}

进阶下面

function App2() {
  const props = {firstName: 'Ben', lastName: 'Hector'};
  return <Greeting {...props} />;
}
```

## jsx中的chidren

在起始标签内部的内容，会被当做prop.chidren传递给子组件（对于自定义组件标签来说）。children的内容可以是：

#### 字符串

并且会自动压缩空格和换行的，以下结果都是一样。

``` html
<div>Hello world!</div>

<div>

Hello world!

</div>

<MyComponent>Hello world!</MyComponent>

<MyComponent>

Hello world!
</MyComponent>
```

#### jsx标签

常用于嵌套组件。

``` html
<MyContainer>
  <MyFirstComponent />
  <MySecondComponent />
</MyContainer>
```

也可以把字符串、jsx标签一起当做prop.children：

``` html
<div>
  Here is a list:
  <ul>
    <li>Item 1</li>
    <li>Item 2</li>
  </ul>
</div>
```

#### js表达式

常用于在组件内部，结合原生js来渲染prop.children。

``` js
function Item(props) {
  return <li>{props.message}</li>;
}

function TodoList() {
  const todos = ['finish doc', 'submit pr', 'nag dan to review'];
  return (
    <ul>
      {todos.map((message) => <Item key={message} message={message} />)}
    </ul>
  );
}
```

#### 函数

函数也可用作prop.children。

``` js
function Repeat(props) {
  let items = [];
  for (let i = 0; i < props.numTimes; i++) {
    items.push(props.children(i));
  }
  return <div>{items}</div>;
}

function ListOfTenThings() {
  return (
    <Repeat numTimes={10}>
      {(index) => <div key={index}>This is item {index} in the list</div>}
    </Repeat>
  );
}
```

#### 注意：true/false/null/undefined/''

这些当做标签内容是无效的，根本不渲染（除非转换成字符串。eg: string(false)）。

可以利用true/false来动态渲染其他jsx。

``` js
<div>
  {isShow && <Header />}
  <Content />
</div>


<div>
  {props.messages.length > 0 &&
    <MessageList messages={props.messages} />
  }
</div>
```
