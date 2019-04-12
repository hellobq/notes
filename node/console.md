# console

[console](http://nodejs.cn/api/console.html#console_console) 对象：用来在控制台打印一些东西。

标准输出流：console.log() / console.info()

标准错误输出流：console.err() / console.warn()

## console.log() / console.info()

``` js
// 直接向控制台打印
console.log('hello');

// 格式化打印 (当然，也可以实用模板字符串)
let prevMsg = 'hello';
console.log('%s, world', prevMsg);

// 把标准输出打印到 info.log 文件中 (不过这样不好，它会把之前的 log 日志覆盖掉)
node demo.js 1>info.log
```

## console.error() / console.warn()

``` js
// 直接向控制台打印
console.error(
  new Error('error msg1')
);

// 把标准输出打印到 error.log 文件中 (不过这样不好，它会把之前的 log 日志覆盖掉)
node demo.js 2>error.log
```

## console.dir()

在控制台打印对象的内容。（好像和 console.log() 没什么两样）

``` js
const person = {
  name: 'Jack',
  showName () {
    return this.name
  }
};
console.dir(
  person
);
console.log(
  person
)
```

## console.time() / console.timeEnd()

统计一段代码的执行时间。

``` js
console.time('for loop')

for (let i = 0; i < 10000; ++i) {}

console.timeEnd('for loop')

// for loop: 0.52ms
```

## console.trance()

当前位置所处的栈信息作为标准错误信息输出。

``` js
console.trace(
  'demo console.trace()'
)

/*
  Trace: demo trace
    at Object.<anonymous> (C:\Users\hello\Desktop\my-notes\demo.js:22:9)
    at Module._compile (internal/modules/cjs/loader.js:688:30)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:699:10)
    at Module.load (internal/modules/cjs/loader.js:598:32)
    at tryModuleLoad (internal/modules/cjs/loader.js:537:12)
    at Function.Module._load (internal/modules/cjs/loader.js:529:3)
    at Function.Module.runMain (internal/modules/cjs/loader.js:741:12)
    at startup (internal/bootstrap/node.js:285:19)
    at bootstrapNodeJSCore (internal/bootstrap/node.js:739:3)
*/
```
