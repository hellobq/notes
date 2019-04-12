# events 事件触发器

node 是事件驱动，所以 node 中许多可触发事件的对象都继承了 [EventEmitter](http://nodejs.cn/api/events.html#events_class_eventemitter) 类的（或者子类的）实例对象，EventEmitter 类是由 [events](http://nodejs.cn/api/events.html#events_events) 模块定义的：

``` js
const
  EventEmitter = require('events'),
  http = require('http');

const server = http.createServer();
console.log(
  server instanceof EventEmitter
);
```

## EventEmitter 类的 on/addListener、emit、off

    emitter.on/addListener(eventName, listener)
    emitter.emit(eventName)
    emitter.off(eventName, listener)

对指定事件 eventName 绑定事件监听函数 listener，通过 emit 触发事件（可携带参数），可用 off 注销事件：

``` js
const EventEmitter = require('events');
class MyEmitter extends EventEmitter{};
const myEmitter = new MyEmitter();
myEmitter.on('event-name', payload => {
  console.log(payload)
  console.log('自定义事件触发了...');
});
myEmitter.emit('event-name', { payload: 'payload-msg' });

```

可使用 on/addListener 为同一个事件注册多个事件处理函数，事件触发时，函数执行顺序取决于注册顺序：

``` js
const EventEmitter = require('events');
class MyEmitter extends EventEmitter{};
const myEmitter = new MyEmitter();
const listener1 = payload => {
  console.log(payload)
  console.log('事件监听函数1触发了...');
}
const listener2 = payload => {
  console.log(payload)
  console.log('事件监听函数2触发了...');
}
myEmitter.on('event-name', listener2);
myEmitter.on('event-name', listener1);
myEmitter.emit('event-name', { payload: 'payload-msg' });  // 先触发 listener2，后 listener1
```

## EventEmitter 类的 once

    emitter.once(eventName, listener)

对绑定的事件 eventName，只触发一次事件监听函数 listener。

``` js
const EventEmitter = require('events');
class MyEmitter extends EventEmitter{};
const myEmitter = new MyEmitter();
myEmitter.once('event-name', payload => {
  console.log(payload)
  console.log('自定义事件触发了...');
});
myEmitter.emit('event-name', { payload: 'payload-msg1' });
myEmitter.emit('event-name', { payload: 'payload-msg2' });  // 不会触发
```

## EventEmitter 类的 removeListener/removeAllListeners

    emitter.removeListener(eventName, listener)
    emitter.removeAllListener([eventName])

从事件 eventName 监听器数组中的 listener。
移除 eventName 的所有监听器（也就是事件处理函数）。

``` js
const EventEmitter = require('events');
class MyEmitter extends EventEmitter{};
const myEmitter = new MyEmitter();
const listener1 = payload => {
  console.log(payload)
  console.log('事件监听函数1触发了...');
}
const listener2 = payload => {
  console.log(payload)
  console.log('事件监听函数2触发了...');
}
myEmitter.on('event-name', listener2);
myEmitter.on('event-name', listener1);
myEmitter.removeListener('event-name', listener2)  // 移除了事件处理函数 listener2
myEmitter.emit('event-name', { payload: 'payload-msg' });

myEmitter.removeAllListeners(['event-name']); // 移除了事件 event-name 所有事件处理函数
myEmitter.emit('event-name', { payload: 'payload-msg' });  // 不再执行任意一个函数
```

## EventEmitter 类本身的事件 newListener/removeListener

EventEmitter (或子类)的实例在添加新的监听器到监听器数组之前，会触发本身的 newListener 事件；

EventEmitter (或子类)的实例在移除指定监听器之后，会触发本身 removeListener 事件。

``` js
const EventEmitter = require('events');
class MyEmitter extends EventEmitter{};
const myEmitter = new MyEmitter();
const prevListener = () => {
  console.log('将要添加新的监听器...')
};
const listener = payload => {
  console.log(payload);
  console.log('事件监听函数触发了...');
}
const nextLisener = () => {
  console.log('已经移除一个注册器了...')
};
myEmitter.on('removeListener', nextLisener);
myEmitter.on('newListener', prevListener);
myEmitter.on('event-name', listener);
myEmitter.removeListener('event-name', listener);
```

#### emitter 是按照顺序执行事件，如果有新的事件，转而处理新的事件，处理完成后接着处理刚才的事件。

``` js
const EventEmitter = require('events');
class MyEmitter extends EventEmitter{};
const myEmitter = new MyEmitter();
const listener11 = () => {
  console.log('event-name1事件 监听函数11 触发了...start..');
  myEmitter.emit('event-name2')
  console.log('event-name1事件 监听函数11 触发了...end..')
}
const listener12 = () => {
  console.log('event-name1事件 监听函数12 触发了...');
}
const listener21 = () => {
  console.log('event-name2事件 监听函数21触发了...');
}
myEmitter.on('event-name1', listener11);
myEmitter.on('event-name1', listener12);
myEmitter.on('event-name2', listener21);
myEmitter.emit('event-name1');

/*
  event-name1事件 监听函数11 触发了...start..
  event-name2事件 监听函数21触发了...
  event-name1事件 监听函数11 触发了...end..
  event-name1事件 监听函数12 触发了...
*/
```
