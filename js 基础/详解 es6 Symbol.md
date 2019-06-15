### 详解 es6 Symbol

es6 新增的 Symbol 用来创建唯一的值。Symbol 属于基本数据类型，不需要使用 new 来创建。

``` js
console.log( Symbol(1) === Symbol(1) ); // false
```

创建 Symbol 值时，传入的参数会先调用 toString 方法：

``` js
console.log( Symbol({a: 1}) ); // Symbol([object Object])
```

Symbol 类型的变量，可以转换成 string、boolean：

``` js
let a = Symbol(1);
console.log(a.toString()); // a + '' 会报错
console.log(Boolean(a), !!a); // true
```

Symbol 用来作为唯一的 key：

``` js
const s = Symbol(1);

let obj = {
  [s]: 1
};

obj[s] = 'string';

console.log( obj[s] );
```

### 字面量对象属性的遍历：

ES6 一共有 5 种方法可以遍历对象的属性。

（1）for...in

for...in循环遍历对象自身的和继承的可枚举属性（不含 Symbol 属性）。

（2）Object.keys(obj)

Object.keys返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 属性）的键名。

（3）Object.getOwnPropertyNames(obj)

Object.getOwnPropertyNames返回一个数组，包含对象自身的所有属性（不含 Symbol 属性，但是包括不可枚举属性）的键名。

（4）Object.getOwnPropertySymbols(obj)

Object.getOwnPropertySymbols返回一个数组，包含对象自身的所有 Symbol 属性的键名。

（5）Reflect.ownKeys(obj)

Reflect.ownKeys返回一个数组，包含对象自身的所有键名，不管键名是 Symbol 或字符串，也不管是否可枚举。

以上的 5 种方法遍历对象的键名，都遵守同样的属性遍历的次序规则。

首先遍历所有数值键，按照数值升序排列。<br>
其次遍历所有字符串键，按照加入时间升序排列。<br>
最后遍历所有 Symbol 键，按照加入时间升序排列。<br>
Reflect.ownKeys({ [Symbol()]:0, b:0, 10:0, 2:0, a:0 })<br>
// ['2', '10', 'b', 'a', Symbol()]

上面代码中，Reflect.ownKeys 方法返回一个数组，包含了参数对象的所有属性。这个数组的属性次序是这样的，首先是数值属性 2 和 10，其次是字符串属性 b 和 a，最后是 Symbol 属性。

### Symbol 的静态方法

Symbol.for 同是创建 Symbol 值，与 Symbol 不同的是：如果参数一样，那么这两个 Symbol 相等。

``` js
Symbol(1) === Symbol(1) // false
Symbol.for(1) === Symbol.for(1) // true
```

Symbol.keyFor 接收由 Symbol.for 创建的 Symbol 值作为参数，返回标识。

``` js
const s = Symbol.for(1);
Symbol.keyFor(s); // '1'
```

### 相关链接
- [阮一峰 es6](https://es6.ruanyifeng.com/#docs/object)
