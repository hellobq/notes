### forEach 跳出循环

默认情况下，`forEach` 遍历数组时，只能通过 `return` 语句实现跳过本次循环，但是不能跳出循环。解决的办法有：

### 1. try catch

在要跳出的循环语句中抛出错误，会中断当前地循环，走 `catch` 代码块内，从而实现 `forEach` 跳出循环的效果。

```
const nums = new Array(10).fill(0);

try {
  nums.forEach((item, idx) => {
    // 索引是 nums.length / 2 时，跳出循环
    if (idx == nums.length / 2 | 0) {
      throw new Error('break')
    }

    console.log('forEach', idx);
  });
} catch(e) {}
```

### 2. 使用其他 API 代替 forEach，比如：some、every

> Array.prototype.some 回调的返回值为 true时，跳出循环;<br>
> Array.prototype.every 回调的返回值为 false 时，跳出循环；

```
const nums = new Array(10).fill(0);

nums.some((item, idx) => {
  if (idx == nums.length / 2 | 0) return true;
  console.log('some', idx);
});

nums.every((item, idx) => {
  if (idx == nums.length / 2 | 0) return false;
  console.log('one', idx);
  return true;
});
```

### 3. for、while、do...while

这些原生的循环，通过 `break` 关键词轻松实现跳出循环。

```
const nums = new Array(10).fill(0);

for (let i = 0; i < nums.length; ++i) {
  if (i == nums.length / 2 | 0) {
    break;
  }
  console.log('for', i);
}

let i = 0;
do {
  console.log(i);
  ++i;
} while (i != nums.length / 2 | 0)
```
