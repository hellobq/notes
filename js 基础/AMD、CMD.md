# AMD、CMD

两种模块规范，主要用来异步加载模块。主要区别是：模块定义和加载时机不同。

#### 1. AMD 前置依赖

如果模块 c.js 分别依赖 a.js、b.js，那么在定义模块 c.js 时，就应该把 a.js、b.js 写在前面：

``` js
define(['a.js', 'b.js'], function (a, b) {
  // ...
})
```

这样，等到 a.js、b.js 加载完成之后，再执行 c.js。

#### 2. CMD 就近依赖

如果模块 c.js 中，和上述一样要使用 a.js、b.js，在使用的时候再引入，别再一开始引入：

``` js
define(function(require, exports, module) {
  let a = require('a.js')
  console.log(a)

  // ...

  let b = require('b.js')
  console.log(b)
})
```

这样，可以直接使用 c.js，等用到 a.js、b.js 时，再加载。
