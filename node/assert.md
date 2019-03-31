# assert

用来校验参数

## assert.deepStrictEqual(actual, expected[, message])

类型相同，值也相等。

    const assert = require('assert')

    const obj1 = {
      a: 1,
      b: [2, true, null, {
        c: {
          d: 3
        }
      }]
    }

    const obj2 = {
      a: 1,
      b: [2, true, null, {
        c: {
          d: 3
        }
      }]
    }

    assert.deepStrictEqual(obj1, obj2, 'obj1 !== obj2')

    // 当obj1 和 obj2 类型或值不同时，会报错，错误信息为：obj1 !== obj2

学习链接：[assert 源码](https://github.com/nodejs/node/blob/master/lib/assert.js)
