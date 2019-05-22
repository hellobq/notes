### 1. 简介 Padding

设置内边距，添加一段空白区域。

``` dart
const Padding({
  Key key,
  @required this.padding,
  Widget child,
})
```

由上源码可知：这个 Widget 的 padding 属性必须设置（通过 `EdgeInsets` 设置的常量值），不能为空。

另外：
- 相对 Container 设置 padding 属性，Padding 更加轻量。
- 相对于 `Padding`，Flutter 并没有为 margin 单独设置一个组件，并且在 `Container` 源码中, margin 属性都是通过 Padding 设置的：

```dart
if (margin != null)
  current = new Padding(padding: margin, child: current);
```

### 2. Padding 类的继承关系

    Object > Diagnosticable > DiagnosticableTree > Widget > RenderObjectWidget > SingleChildRenderObjectWidget > Padding

SingleChildRenderObjectWidget 规定 Padding 只能包裹一个子部件。

### 3. Padding 的布局行为

- 如果子部件为 null, 会产生一个宽为 left+right、高为 top+bottom 的区域。
- 如果子部件不为空，会经历三个过程：调整 child 尺寸、调整 child 位置、调整 Padding 尺寸，从而达到最终效果。

源码如下：

``` dart
if (child == null) {
  size = constraints.constrain(new Size(
    _resolvedPadding.left + _resolvedPadding.right,
    _resolvedPadding.top + _resolvedPadding.bottom
  ));
  return;
} else {
  // 调整child尺寸
  final BoxConstraints innerConstraints = constraints.deflate(_resolvedPadding);
  child.layout(innerConstraints, parentUsesSize: true);

  // 调整child位置
  final BoxParentData childParentData = child.parentData;
  childParentData.offset = new Offset(_resolvedPadding.left, _resolvedPadding.top);

  // 调整Padding尺寸
  size = constraints.constrain(new Size(
    _resolvedPadding.left + child.size.width + _resolvedPadding.right,
    _resolvedPadding.top + child.size.height + _resolvedPadding.bottom
  ));
}
```
