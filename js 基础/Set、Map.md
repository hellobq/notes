# Set、Map

集合和字典，[es2015](es6.ruanyifeng.com) 新引入的两种数据结构，主要用作数据去重和数据存储。

## 创建 Set 实例

    new Set([iterable])

创建 set 的唯一方式：构造函数 `Set`。可使用一数组用来初始化 set 实例，利用其内部可自动去重的特性，可帮助数组去重。

``` js
const set = new Set([1, 2, 4, 2, 3]);

[...set]    // [1, 2, 4, 3]
new Set([{}, {}, NaN, NaN, +0, -0])    // Set { {}, {}, NaN, 0 }
```

**注意**：在 set 内，NaN 被看作相等的，即使它不和自己相等。

### Set 实例的属性

    Set.prototype.size   获取 set 实例长度
    Set.prototype.constructor   获取 set 实例的构造函数

### Set 实例的操作方法

    Set.prototype.has(v)    判断 v 是不是 set 的成员
    Set.prototype.add(v)    往 set 添加新的成员 v
    Set.prototype.delete(v)    从 set 成员内删除 v
    Set.prototype.clear()    清空 set 成员

### Set 实例的遍历方法

    Set.prototype.values()    获取 set 所有成员键名
    Set.prototype.keys()    获取 set 所有成员的键值
    Set.prototype.entries()    获取 set 所有成员的键名和键值

三者返回的对象都是 Iterator 遍历，都可被 for...of 遍历。不过都没卵用，如果要遍历 set 实例，直接使用 for...of 遍历即可，何必再调用实例方法呢。

### set 实例转数组

    Array.from(set)
    [...set]

## Map

字典，也就是一个个的键值对儿。并且其中的键不会像对象的属性一样自动被 String 转变（解决属性相同导致覆盖的问题）。

### 创建 map 实例

    new Map([iterable])

可使用数组将其初始化，数组的成员是表示一个个键值对的数组。

``` js
console.log(
  new Map([
    [{}, 1],
    [{}, 2],
    [{ name: 'haha' }, 'lala'],
    ['name', 'Baiq'],
    ['age', 20]
  ])
);

/*
  Map {
    {} => 1,
    {} => 2,
    { name: 'haha' } => 'lala',
    'name' => 'Baiq',
    'age' => 20
  }
*/
```

### Map 实例的属性

    Map.prototype.size    返回 map 结构的成员数量
    Map.prototype.constructor   获取 Map 实例的构造函数

### Map 实例的操作方法

    Map.prototype.has(k)    判断键名是k的键值对儿是不是 map结构的成员
    Map.prototype.set(k, v)    往 map 结构中添加新的成员 k => v
    Map.prototype.delete(k)    从 map 结构内删除键名为 k 的成员
    Map.prototype.clear()    清空 map 结构

### Map 实例的遍历方法

    Map.prototype.values()    获取 Map 结构所有成员键名
    Map.prototype.keys()    获取 Map 结构所有成员的键值
    Map.prototype.entries()    获取 Map 结构所有成员的键名和键值

``` js
for (let [k, v] of map.entries()) {
  console.log(k, v)
}
```

### Map 实例转数组

    [...map.keys()]
    [...map.values()]
    [...map.entries()]/[...map]    二维数组

    
### demo: 计算字母 'hello' 各个字母的个数

``` js
const 
  str = 'hello',
  map = new Map(),
  obj = {};

for (let ch of str) {
  map.set(
    ch, 
    map.has(ch) ? map.get(ch) + 1 : 1
  );
}

for (let [k, v] of map) {
  obj[k] = v;
}

console.log(obj);
// { h: 1, e: 1, l: 2, o: 1 }
```

### WeakMap 和 Map 的区别

1. WeakMap 只接受对象作为键名，否则报错。不计入垃圾回收机制。
2. WeakMap 不是 Iterator 对象，不能使用 for...in 遍历。


### WeakSet 和 Set 的区别

1. WeakSet 的每个成员都是对象引用，否则报错。对象不计入垃圾回收机制。
2. WeakSet 不是 Iterator 对象，不能使用 for...in 遍历。


相关链接：
- [MDN - Set](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set)
- [MDN - WeakSet](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/WeakSet)
- [MDN - Map](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Map)
- [MDN - WeakMap](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/WeakMap)
- [阮一峰 Set、Map](http://es6.ruanyifeng.com/#docs/set-map)
- [原生实现 Set、Map](https://juejin.im/post/5acc57eff265da237f1e9f7c#heading-11)

