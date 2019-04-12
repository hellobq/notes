# Buffer

[Buffer](http://nodejs.cn/api/buffer.html#buffer_buffer) 是一个 node 内置类，用来在内存中开辟一片区域，来缓存二进制数据。

Buffer 类位于全局作用域，直接使用，不需要 `require('buffer').Buffer`。

### Buffer 用在什么场景？

当需要缓存二进制数据时，就需要用到 Buffer，比如：TCP 流、文件系统操作等。

### 创建 buf: 已知需要缓存的数据

    Buffer.from(obj) obj可以是：Array、String、Buffer等。
    Buffer.from(Array)
    Buffer.from(String[, encoding])
    Buffer.from(Buffer)

``` js
const buf = Buffer.from([0x62, 0x75, 0x66, 0x66, 0x65, 0x72]);

console.log(
  buf
);
// <Buffer 62 75 66 66 65 72>


const buf1 = Buffer.from('buffer');
const buf2 = Buffer.from(buf1);

buf1[0] = 0x61;

console.log(
  buf1,
  buf2
);
// <Buffer 61 75 66 66 65 72> <Buffer 62 75 66 66 65 72>
```

### 创建 buf: 未知需要缓存的数据，需要事先开辟一段大小的内存

    Buffer.alloc(size[, fill=0][, encoding=utf8])

``` js
const buf = Buffer.alloc(5, 'a');

console.log(buf);
// <Buffer 61 61 61 61 61>
```

另外：[Buffer.allocUnsafe](http://nodejs.cn/api/buffer.html#buffer_class_method_buffer_allocunsafe_size)、[Buffer.allocUnsafeSlow](http://nodejs.cn/api/buffer.html#buffer_class_method_buffer_allocunsafeslow_size)，alloc -> allocUnsafe -> allocUnsafeSlow 创建速度依次变大，但是 alloc 最安全，因为 alloc 能确保新创建的 buf 不会包含敏感数据。

### buf 转字符串

    Buffer.from(str)
    buf.toString([encoding=utf8][, start=0][, end=buf.length])
  
``` js
const buf = Buffer.from('test');

console.log(
  buf,
  buf.toString(),
  buf.toString('utf8', 0, 3)
);
// <Buffer 74 65 73 74> 'test' 'tes'
```

### buf 转 json

    buf.toJSON()

``` js
const 
  buf1 = Buffer.from([1, 2, 10, 199]),
  buf2 = Buffer.from('test');

console.log(
  buf1.toJSON(),
  buf2.toJSON()
);
// { type: 'Buffer', data: [ 1, 2, 10, 199 ] } { type: 'Buffer', data: [ 116, 101, 115, 116 ] }
```

### buf 长度、裁剪

    buf.length、buf.slice([beg=0][, end=buf.length])

``` js
const buf = Buffer.from('test哈');

console.log(
  buf,
  buf.length,
  buf.slice(1).toString()
);
// <Buffer 74 65 73 74 e5 93 88> 7 'est哈'
```

#### buf 比较是否相等。比较的是字节

    buf.equals(otherBuf)

如果字节完全相同，为 true。

```js
const 
  buf1 = Buffer.from('ABC'),
  buf2 = Buffer.from('414243', 'hex');

console.log(
  buf1.equals(buf2)
);
// true
```

### Buffer 合并

    buf.concat([buf1, buf2...][, totalLength])

``` js
const 
  buf1 = Buffer.alloc(10),
  buf2 = Buffer.alloc(14),
  buf3 = Buffer.alloc(18);

// 顺便计算 newBuf 长度，省了二次遍历原buf
const totalLength = buf1.length + buf2.length + buf3.length;

const bufA = Buffer.concat([buf1, buf2, buf3]);

console.log(
  bufA,
  bufA.length
);
// <Buffer 00 00 ...> 42
```

### 用 buf.fill()方法来清空 buf

    buf.fill(0)

### 判断 buf 是否包含特殊值

    buf.indexOf() / buf.includes()

``` js
const buf = Buffer.from('我要清空buf');

console.log(
  buf.includes('空'),
  buf.indexOf('空')
);
// true 9
```

### Buffer 类和 buffer 模块

    require('buffer').Buffer === Buffer

### 释放 buf 内存空间

只能由 V8 释放，用户只需删除对 buf 的引用即可。

相关链接：
- [Buffer 详解](https://juejin.im/post/5afd57e851882542ac7d76af#heading-18)
- [菜鸟教程 Buffer](http://www.runoob.com/nodejs/nodejs-buffer.html)
