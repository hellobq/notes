### 可滚动 widgets 简介

默认情况：当内容超过显示视口( ViewPort )时，如果没有特殊处理，Flutter 则会提示 Overflow 错误。解决它，就把布局设置可滚动类型。

Flutter 提供了多种可滚动 widget（Scrollable Widget）用于显示列表和长布局。这些可滚动 Widgets 都直接或间接包含一个 Scrollable widget，因此它们包括一些共同的属性：

``` dart
Scrollable({
  ...
  this.axisDirection = AxisDirection.down, // 滚动方向
  this.controller,
  /*
    控制滚动位置和监听滚动事件。
    
    默认情况下，widget树中会有一个默认的PrimaryScrollController，如果子树中的可滚动widget没有显式的指定controller并且primary属性值为true时（默认就为true），可滚动widget会使用这个默认的PrimaryScrollController。
    
    这种机制带来的好处是父widget可以控制子树中可滚动widget的滚动，例如，Scaffold使用这种机制在iOS中实现了"回到顶部"的手势。我们将在本章后面“滚动控制”一节详细介绍ScrollController。
  */
  this.physics,
  /*
    决定可滚动Widget如何响应用户操作，比如用户滑动完抬起手指后，继续执行动画；或者滑动到边界时，如何显示。
      默认情况下，Flutter会根据具体平台分别使用不同的 ScrollPhysics 对象，应用不同的显示效果；
      如当滑动到边界时，继续拖动的话，在iOS上会出现弹性效果，而在Android上会出现微光效果。
      如果你想在所有平台下使用同一种效果，可以显式指定，Flutter SDK中包含了两个 ScrollPhysics 的子类可以直接使用：
        ClampingScrollPhysics：Android下微光效果。
        BouncingScrollPhysics：iOS下弹性效果。
  */
  @required this.viewportBuilder, 
})
```

### ScrollBar

Scrollbar 是一个 Material 风格的滚动指示器（滚动条），如果要给可滚动 widget 添加滚动条，只需将 Scrollbar 作为可滚动 widget 的父 widget 即可，如：

``` dart
Scrollbar(
  child: SingleChildScrollView(
    ...
  ),
)
```

CupertinoScrollbar 是 iOS 风格的滚动条，如果你使用的是 Scrollbar，那么在 iOS 平台它会`自动切换`为 CupertinoScrollbar。

Scrollbar 和 CupertinoScrollbar 都是通过 ScrollController 来监听滚动事件来确定滚动条位置。

### 主轴和纵轴

在可滚动 widget 的坐标描述中，通常将滚动方向称为主轴，非滚动方向称为纵轴。由于可滚动 widget 的默认方向一般都是沿垂直方向，所以默认情况下 `主轴就是指垂直方向，水平方向同理`。
