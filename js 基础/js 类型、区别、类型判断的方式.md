### `js 类型、区别`

js 类型：分为值类型和引用类型。
- 值类型：number、string、boolean、null、undefined、symbol（创建变量时，不需要使用 new）；
- 引用类型：object（对象、函数、数组）

值类型和引用类型的区别
- 变量的存储区域不同：
  - 值类型的变量是存放在栈内存的，变量标识符和变量值都放在栈内存。所占内存少且快。
  - 引用类型的变量是存放在栈内存和堆内存中的。变量标识符存储在栈内存（引用地址），变量值放在堆内存，大存储而慢。
- 变量的比较方式不同：
  - 值类型的变量是值比较。
  - 引用类型的变量是比较引用地址（对于每个不同的对象，存储堆内存的地址是不同的）。
- 函数传参时的表现不同：
  - 值类型的变量是值传递。
  - 引用类型的变量是址传递。

### `typeof`

可通过 typeof 判断变量是否是某个值类型。注意：
- typeof null 结果是 object；
- typeof 函数名 结果是 function；

### `instanceof`

可通过 instanceof 判断引用类型。注意：
- 考虑到继承。若类 B 继承于类 A，B 的实例 b：`b instanceof B === true 同时 b instanceof A === true`；
- Function 和 Object 的微妙关系；
- 如何实现一个 instanceof ？

  ``` js
  function myInstanceof(instance, Constructor) {
    while (instance !== null) {
      if (instance.constructor === Constructor) {
        return true;
      }
      instance = instance.__proto__
    }

    return false;
  }
  ```

考虑：`Object instanceof Function，Function instanceof Object，Object instanceof Object`？

因为 `Object` 是一个构造函数，所以它是 `Function` 的实例，又因为 `Function` 是这个构造函数本质是对象，它又是 `Object` 的实例，因此以上表达式都是 `true`。

### `({}).toString.call(val)`

上述表达式可判断任何数据类型，可看作升级版的 `instanceof`，也可这样写：`Object.prototype.toString.call(val)`，它等于 `[object Constructor-val]`。
