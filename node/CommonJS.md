# CommonJS

它是一种模块化方式。

## 和主流的esMoudle不同

+ 是两种不同的模块引入方式。module.exports/require export/import

+ 出现的时间不同：esmodule比CommonJS晚。

+ default是esmodule独有的，在CommonJs中则没有。

## 导入导出

可以把exports看作是module.exports的引用；require引用时可用结构。

``` js
// demo1.js
module.exports = x \<any\>

exports.a = a

exports.b = b

module.exports = {
  a,
  b
}

// demo2.js
const x = require('./demo1')
const { a, b } = require('./demo1')

```
