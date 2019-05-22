### 1. Container 的构造函数

用来创建一个 `盒子` 的部件，使用其样式属性进行修饰内容，`Container` 的构造函数如下：

``` dart
(new) Container({
  Key key,
  AlignmentGeometry alignment,
  EdgeInsetsGeometry padding,
  Color color,
  Decoration decoration,
  Decoration foregroundDecoration,
  double width,
  double height,
  BoxConstraints constraints,
  EdgeInsetsGeometry margin,
  Matrix4 transform,
  Widget child
}) → Container
```

### 1.1. key：Container唯一标识符，用于查找更新。

### 1.2. alignment 设置子部件的对其方式

通过 `Alignment` 类给 `alignment` 属性赋值。
- Alignment(-1.0, -1.0) 上左
- Alignment(0.0, -1.0) 上中
- Alignment(1.0, -1.0) 上右
- Alignment(-1.0, 0.0) 中左
- Alignment(0.0, 0.0) 中心
- Alignment(1.0, 0.0) 中右
- Alignment(-1.0, 1.0) 下左
- Alignment(0.0, 1.0) 下中
- Alignment(1.0, 1.0) 下右

类似地，使用继承于 `Alignment` 的子类 `FractionalOffset`，也能直接规定子部件的对齐方式（Alignment 也有以下静态属性）：
- FractionalOffset.topLeft
- FractionalOffset.topCenter
- FractionalOffset.topRight
- FractionalOffset.centerLeft
- FractionalOffset.center
- FractionalOffset.centerRight
- FractionalOffset.bottomLeft
- FractionalOffset.bottomCenter
- FractionalOffset.bottomRight

这两者都是用来标识子部件的对齐方式，区别是：`Alignment` 是以矩形中心为坐标系原点；`FractionalOffset` 则以矩形左上角为坐标系原点。官方主推使用 `Alignment`（大概它能使用 0.5 吧）。

### 1.3. padding / margin 给 Container 内部增加内外空白空间

通过 `EdgeInsets` 设置的常量值，给 `padding / margin` 属性赋值。若仅仅设置内边距，亦可使用 `Padding`。

### 1.4. color 设置 Container 的背景色

可通过 `Colors/Color` 类指定颜色值。

``` dart
Colors.red
Colors.red[400]  // 指定透明度
Colors.red.shade400 // 同上

Color(0xFFFFFFFF) // 必须是8位的16进制
Color.fromARGB(0xFF, 0x42, 0xA5, 0xF5) // Alpha Red Green Blue
Color.fromARGB(255, 66, 165, 245)
Color.fromRGBO(66, 165, 245, 1.0); // Red Green Blue Opacity
```

注意：当 Container 设置了 `decoration` 属性时，不能再设置该属性。因为在 `decoration` 中有设置背景色的属性了。

### 1.5. decoration / foregroundDecoration

两者属性值可以是以下类的实例：`BoxDecoration`、`FlutterLogoDecoration`、`ShapeDecoration`、`UnderlineTabIndicator`

就 `BoxDecoration` 举例：

``` dart
// 设置背景色、边框
Container(
  decoration: BoxDecoration(
    color: Colors.red[400],
    border: Border(
      left: BorderSide(color: Colors.blue),
      top: BorderSide(color: Colors.pink),
      right: BorderSide(color: Colors.red),
      bottom: BorderSide(color: Colors.green)
    )
  )
)
```
decoration 和 foregroundDecoration 是填充配置，前者是在子部件之下，后者是子部件之上，可以设置填充颜色，边框，填充形状，阴影，渐变色，背景图片等。

### 1.6. width / height

当 `Container` 有子部件时，`Container` 宽高的默认值是 `auto`，即它的宽高由子部件撑开的；当没有子部件时，宽高默认是无限大（double.infinity）。

也可显式地设置其宽高：

``` dart
// 使 Container 的宽高撑满父元素
Container(
  width: double.infinity,
  height: double.infinity
)
```

倘若只设置部件宽高：可用 `SizedBox` 代替 `Container`。

### 1.7. constraints 设置 Container 占据的最大/最小的空间

使用 `BoxConstraints` 示例给 `constraints` 属性赋值：

``` dart
constraints: BoxConstraints(
  maxHeight: 180.0,
  maxWidth: 180.0,
  minWidth: 150.0,
  minHeight: 150.0
)
```

### 1.8. transform 设置 Container 的变换矩阵

变换包括：缩放、旋转、偏移。通过 类 `Matrix4` 来设定。

``` dart
import 'package:flutter/material.dart';
import 'dart:math';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Container demo')
        ),
        body: Center(
          child: Container(
            width: 200.0,
            height: 200.0,
            color: Colors.blue[300],
            alignment: Alignment(0.0, 0.0),

            // 按照 Z 轴旋转45°  要导包 import 'dart:math'
            transform: Matrix4.rotationZ(pi / 4),
            child: Text('Container Text!')
          )
        )
      )
    );
  }
}
```
### 1.9. child 用于设置 Container 的子部件


### 2. Container 渲染过程

transform -> decoration -> child -> foregroundDecoration

### 3. Container 的继承关系

Object > Diagnosticable > DiagnosticableTree > Widget > StatelessWidget > Container

### 4. Container 使用场景

- 设置背景色
- 设置内/外边距（如果仅是内边距也可用 Padding）
- 设置对齐方式（Align 也能实现）
- 设置背景图（也可用嵌套布局 Stack）
- 设置圆角（也可使用 ClipRect/CircleAvatar）与边框
- 设置部件宽高（也可使用 SizedBox）。

**采坑**：
- Container 内嵌套 InkWell 时，当触发 InkWell 的 onTap 实践时没有涟漪效果，可在 InkWell 外套一层 `Material`，如下代码所示：

``` dart
child: Container(
  width: 200.0,
  height: 200.0,
  color: Colors.blue[300],
  alignment: Alignment(0.0, 0.0),
  transform: Matrix4.rotationZ(pi / 4),
  child: Material(

    // 去除 Material 自带的背景色
    color: Colors.transparent,
    child: InkWell(
      onTap: (){},
      child: Text('哈哈哈')
    )
  )
)
```

### 5. Container 源码

``` dart
@override
  Widget build(BuildContext context) {
    Widget current = child;

    if (child == null && (constraints == null || !constraints.isTight)) {
      current = new LimitedBox(
        maxWidth: 0.0,
        maxHeight: 0.0,
        child: new ConstrainedBox(constraints: const BoxConstraints.expand())
      );
    }

    if (alignment != null)
      current = new Align(alignment: alignment, child: current);

    final EdgeInsetsGeometry effectivePadding = _paddingIncludingDecoration;
    if (effectivePadding != null)
      current = new Padding(padding: effectivePadding, child: current);

    if (decoration != null)
      current = new DecoratedBox(decoration: decoration, child: current);

    if (foregroundDecoration != null) {
      current = new DecoratedBox(
        decoration: foregroundDecoration,
        position: DecorationPosition.foreground,
        child: current
      );
    }

    if (constraints != null)
      current = new ConstrainedBox(constraints: constraints, child: current);

    if (margin != null)
      current = new Padding(padding: margin, child: current);

    if (transform != null)
      current = new Transform(transform: transform, child: current);

    return current;
  }
  ...
```

### 6. 相关连接：
- [Flutter 入门  — Container 属性详解](https://juejin.im/post/5b3c27a3e51d4519475ee8d8#heading-5)
- [Flutter 入门，Container 详解](https://juejin.im/post/5b13c3e1f265da6e3d666d80)
- [Container Class](https://api.flutter.dev/flutter/widgets/Container-class.html)
