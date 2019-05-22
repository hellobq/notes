### 1.1 简介 Align

Align 部件用来设置子部件的对齐方式，并根据子部件的尺寸来调节自己的尺寸。

`Container` 中的 `alignment` 属性也是通过 Align 实现的:

``` dart
if (alignment != null)
  current = new Align(alignment: alignment, child: current);
```

### 1.2 Align 的继承关系

    Object > Diagnosticable > DiagnosticableTree > Widget > RenderObjectWidget > SingleChildRenderObjectWidget > Align

Align 和 Padding 类似，基础而单一。

### 1.3 Align 的用法

    (new) Align({
      Key key,
      AlignmentGeometry alignment: Alignment.center,
      double widthFactor,
      double heightFactor,
      Widget child
    }) → Align

widthFactor：宽度因子，如果设置的话，Align的宽度就是child的宽度乘以这个值，不能为负数（用得少）。

heightFactor：高度因子，如果设置的话，Align的高度就是child的高度乘以这个值，不能为负数（用得少）。

### 1.4 使用场景总结

Align 部件 alignment 有点用处，但是像 Conatainer、Row、Column 都内置子部件的属性，所以 Align 这种底层的部件用的比较少。

### 2. Center

    Object > Diagnosticable > DiagnosticableTree > Widget > RenderObjectWidget > SingleChildRenderObjectWidget > Align > Center

Center 继承 Align，将 alignment 属性默认设置为 Alignment.center，因此在 Center 源码中没 alignmeng 属性：

``` dart
class Center extends Align {
  /// Creates a widget that centers its child.
  const Center({ Key key, double widthFactor, double heightFactor, Widget child })
    : super(key: key, widthFactor: widthFactor, heightFactor: heightFactor, child: child);
}
```

### 相关链接
- [详解 Padding、Align、Center](https://github.com/yang7229693/flutter-study/blob/master/post/5.%20Flutter%20%E5%B8%83%E5%B1%80%EF%BC%88%E4%BA%8C%EF%BC%89-%20Padding%E3%80%81Align%E3%80%81Center%E8%AF%A6%E8%A7%A3.md)
