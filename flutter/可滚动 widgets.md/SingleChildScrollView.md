### SingleChildScrollView

SingleChildScrollView 类似于  Android中的 ScrollView 或 RN 中的 ScrollView，它只能接收一个子 Widget。定义如下：

``` dart
SingleChildScrollView({
  this.scrollDirection = Axis.vertical, //滚动方向，默认是垂直方向
  this.physics, 
  this.controller,

  this.child,
  this.reverse = false, 
  this.padding, 
  bool primary, 
})
```

注意：通常 SingleChildScrollView 只应在期望内容适合屏幕的情况下使用，它无法使用基于 Sliver 的延迟实例化，如果预计视口通常包含超出屏幕尺寸的内容，那么 SingleChildScrollView 将会非常昂贵。一句话：`SingleChildScrollView` 不适合动态渲染内容。

### SingleChildScrollView demo:

``` dart
Scrollbar(
  child: SingleChildScrollView(
    physics: BouncingScrollPhysics(), // 统一为 IOS 回弹效果
    padding: EdgeInsets.all(16.0),
    child: Center(
      child: Column( 
        children: str.split('').map((item)  => Text('$item', textScaleFactor: 2.0)).toList(),
      ),
    ),
  ),
)
```
