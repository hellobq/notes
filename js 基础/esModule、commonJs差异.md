# esModule、commonJs差异

#### 1. 手写模块导出、引入的方式不同

export/import 

module.exports/require

#### 2. esModule 模块导出时是值的引用，commonJs 模块导出时是值的拷贝。

commonJS 导出的模块：

``` js
// index1.js
let a = 1
function add () {
  a++
}
module.exports = {
  a,
  add
}

// index2.js
const { a, add } = require('./1.js')
console.log(a)  // 1
add()
console.log(a)  // 1
```

esModule 导出的模块：

``` js
// index1.js
export let a = 1
export function add () {
  a++
}

// index2.js
import { a, add } from './index1'

console.log(a)  // 1
add()
console.log(a)  // 2
```

#### 3. 模块同步引入时，esModule 不能在业务逻辑内，只能放到文件最顶端，而 require 可以放在业务逻辑内。
