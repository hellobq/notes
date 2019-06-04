### ConstrainedBox、SizedBox

`ConstrainedBox` 限制子部件宽高的最大/最小值；`SizedBox` 用来绘制一个规定宽高的部件。

ConstrainedBox 的构造函数：
``` dart
ConstrainedBox({
  ...
  @required BoxConstraints constraints, 
  Widget child
})
```

由 ConstrainedBox 的构造函数可知，ConstrainedBox 的限制条件是由 BoxConstraints 实例来约束的，BoxConstraints 的构造函数如下：
``` dart
const BoxConstraints({
  this.minWidth = 0.0,
  this.maxWidth = double.infinity, //最大宽度
  this.minHeight = 0.0,
  this.maxHeight = double.infinity //最大高度
})
```

更方便地，BoxConstraints 类提供其他有用的命名构造函数：
- BoxConstraints.tightFor(double width, double height)，它可以生成给定大小的限制；
- const BoxConstraints.expand() 可以生成一个尽可能大的用以填充另一个容器的 BoxConstraints。
- ...

SizedBox 的构造函数：
``` dart
SizedBox(
  ...
  double width, 
  double height, 
  Widget child
)

因为 SizedBox 是 Constrained 的定制，因为上面的构造函数亦等价于：
ConstrainedBox(
  constraints: BoxConstraints.tightFor(
    width: ..
    height: ..
  )
)

```

### 实现一个最小高度为50，宽度尽可能大的红色容器

``` dart
ConstrainedBox(
  constraints: BoxConstraints(
    minHeight: 50.0,
    minWidth: double.infinity
  ),
  child: Container(
    color: Colors.red,
    height: 10.0
  )
)
```

因为 Container 包含 constraints 属性，亦可直接设置：
``` dart
Container(
  color: Colors.red,
  constraints: BoxConstraints(
    minHeight: 50.0
  ),
  height: 10.0,
)
```

### 相关链接
- [flutter ConstrainedBox](https://api.flutter.dev/flutter/widgets/ConstrainedBox-class.html)
- [flutter SizedBox](https://api.flutter.dev/flutter/widgets/SizedBox-class.html)
- [flutter 实战 ConstrainedBox 和 SizedBox](https://book.flutterchina.club/chapter5/constrainedbox_and_sizebox.html)
