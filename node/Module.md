# Module

它是一种模块化方式。核心思想是：通过 require 同步地引入其他模块，通过 module.exports / exports 暴露模块接口。

## module 对象

每个 js 文件（模块）内都默认存在一个 module 对象，它有以下属性：

- id: 模块的id
- exports: 模块导出的内容，默认是 { }
- parent: 引用该模块的父模块
- filename: 包含绝对路径的模块名
- loaded: 模块是否加载完成
- children: 子模块。默认是 [ ]
- paths: 模块搜索路径

## module.exports 和 exports

它们是相同的，即 `module.exports === exports`，都指向同一对象，默认都是 { }。

使用exports = { a } 的方式暴露 a，同时使用const { a } = require('相对路径') 是不可取的，因为 require 默认导入的是通过 module.exports 暴露的接口，但是此时 module.exports === { }; exports === { a }; 它们不再指向同一引用。  

## 和主流的 esMoudle 不同点

+ 模块引入方式是不同的。module.exports/require export/import

+ 出现的时间不同：esmodule比CommonJS晚。

+ CommmonJS 只能同步加载模块，esMoudle 可以实现异步加载。

+ 同步加载模块时，require 可以放到 js 文件任何处，什么是 js 业务逻辑中；import 必须放到文件顶部。

## node 中的循环依赖

并不会导致死循环。例如 a.js 和 b.js 内都暴露一些接口，并且 a.js 和 b.js 存在相关引用的关系。那么执行 `node a` 时，会执行 a.js 和 b.js 的逻辑，但是在执行 b.js 逻辑时，node 发现 b.js 中又引用了 a.js，那么会认为 a.js 并未暴露任何东西（就是默认值：{}）。

    // test.js
    const test1 = require('./test1')
    console.log(1)
    console.log(test1)
    exports.d = 4
    exports.e = 5

    // test1.js
    const test =  require("./test");
    console.log(test)
    exports.a = 1;
    exports.b = 2;
    exports.c = 3;

    /* 
      运行 node test 时，
      执行结果为：{} 1 {a: 1, b: 2, c: 3} 
    */

## node 中可通过 require 引入的文件类型

在任意 js 模块中，打印 require 对象：

    {
      [Function: require]
      resolve: { [Function: resolve] paths: [Function: paths] },
      main: Module {},
      extensions: {
        '.js': [Function], '.json': [Function], '.node': [Function]
      },
      cache: {}
    }

支持引入三种类型文件：.js .json .node

## 模块缓存

在同一个 test1.js 模块内，引用多次同一个其他 test2.js 模块，在第一次引入之后会被缓存。

    // test1.js
    console.log('test1')

    // test2.js
    require('./test1.js')
    require('./test1.js')

    // 在执行 node test2 时，只会打印一次 'test1'

解决方式：把 test2.js 中的业务逻辑放在函数内，暴露出去。

    // test1.js
    module.exports = () => {
      console.log('test1')
    }

    // test2.js
    require('./test1.js')()
    require('./test1.js')()

    //  在执行 node test2 时，只会打印两次 'test1'

学习链接：https://semlinker.com/node-module/
