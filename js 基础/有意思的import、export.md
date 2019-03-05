# import export

import、export 的复合写法。如果import、export 的模块相同，那么可以直接这样写：

#### 1. 部分接口（导出源模块部分内容）

``` js
// index1
const name = 'Jack', age = 20, hex = '男'
export {
  name,
  age,
  hax
}

// index2
export { name, age } from './index1'

等同于

import { name, age } from './index1'
export {
  name,
  age
}
```

**注意**：此时index2.js只是转发作用，在其内部不能使用name, age。

#### 2. 默认接口（以default形式导出）

``` js
// index1
const name = 'Jack', age = 20, hex = '男'
export {
  name,
  age,
  hax
}


// index2
export { name as default } from './index1'

等同于

import { name } from './index1'
export default name
```

#### 3. 整体接口（导出源模块全部内容）

``` js
// index1
const name = 'Jack', age = 20, hex = '男'
export {
  name,
  age,
  hax
}


// index2
export * from './index1'

等同于

import { name, age } from './index1'
export {
  name, age, hex
}
```

#### 4. 具名接口（把源文件default出的模块，改名）

``` js
// index1
const obj = { 
  name: 'Jack', 
  ag: 20,
  hex: '男'
}
export default obj


// index2
export { default as haha } from './index1'

等同于

import { default as haha } from './index1'
export {
  haha
}
```

#### 5. 部分接口 + 改名接口（从源文件中导出部分模块，并在接口中改名）

``` js
// index1
const name = 'Jack', age = 20
export {
  name,
  age
}


// index2
export { name as na } from './index1'

等同于

import { name as na } from './index1'
export {
  na
}
```

## import 

``` js
// 在写  React 类组件时，通常会这样写：
import React, { Component } from 'react'


// 因为在 react 内部是这样导出的：
export default React
export {
  Component,
  Lazy,
  Suspense
  // ....
}
```
