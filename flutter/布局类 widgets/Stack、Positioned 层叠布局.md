### Stack、Positioned 层叠布局

`Stack` 允许子部件堆叠（第 n 个部件会堆叠在第 n - 1 个部件上），`Positioned` 允许子部件定位（作为 Stack 子部件）。从而子部件可以根据父部件四个角的位置来确定自身位置。

Stack 构造函数：
``` dart
Stack({
  this.alignment = AlignmentDirectional.topStart,
  /*
    alignment 决定没有使用 Positioned 进行绝对定位的部件，它以父部件左上角为参考系，left/right 为主轴，top/bottom 为负轴
    在 flutter/Flutter基本部件/Align、Center.md 有描述
  */
  this.textDirection,
  /*
    textDirection: 用于决定alignment对齐的参考系
      TextDirection.ltr：alignment的start代表左，end代表右
      TextDirection.rtl：alignment的start代表右，end代表左
  */
  this.fit = StackFit.loose,
  /*
    fit 用于决定没有定位的子 widget 如何去适应 Stack 的大小
      StackFit.loose：使用子widget的大小
      StackFit.expand：扩伸到Stack的大小
  */
  this.overflow = Overflow.clip,
  /*
    overflow：决定如何显示超出Stack显示空间的子widget
      Overflow.clip：超出部分会被剪裁
      Overflow.visible 不会被剪裁
  */
  List<Widget> children = const <Widget>[],
})
```

Positioned 构造函数：
``` dart
const Positioned({
  Key key,
  this.left, 
  this.top,
  this.right,
  this.bottom,
  this.width,
  this.height,
  /*
    left、top 、right、 bottom分别代表离 Stack 左、上、右、底四边的距离
    width 和 height 用于指定定位元素的宽度和高度
      此处的width、height 和其它地方的意义稍微有点区别，此处用于配合left、top 、right、 bottom来定位widget，举个例子，在水平方向时，你只能指定left、right、width三个属性中的两个，如指定left和width后，right会自动算出(left+width)，如果同时指定三个属性则会报错，垂直方向同理。
  */
  @required Widget child,
})
```

### Stack、Positioned demo 如下：

``` dart
ConstrainedBox(
  constraints: BoxConstraints.expand(),
  // 让子部件占满父部件空间

  child: Stack(
    alignment: Alignment.center,
    children: <Widget>[
      Container(
        child: Text(
          "Hello world",
          style: TextStyle(
            color: Colors.white
          )
        ),
        color: Colors.red,
      ),
      Positioned(
        left: 18.0,
        child: Text("I am Jack"),
      ),
      Positioned(
        top: 18.0,
        child: Text("Your friend"),
      )        
    ],
  ),
)
```

### 相关链接
- [flutter Stack](https://api.flutter.dev/flutter/widgets/Stack-class.html)
- [flutter Positioned](https://api.flutter.dev/flutter/widgets/Positioned-class.html)
- [flutter 实战层叠布局 Stack、Positioned](https://book.flutterchina.club/chapter4/stack.html)
