### SingleChildScrollView

SingleChildScrollView 类似于  Android中的 ScrollView 或 RN 中的 ScrollView，它只能接收一个子 Widget。定义如下：

``` dart
SingleChildScrollView({
  this.scrollDirection = Axis.vertical, //滚动方向，默认是垂直方向
  this.physics, 
  this.controller,

  this.child,
  this.reverse = false, 
  /*
    scrollDirection值为Axis.horizontal，如果阅读方向是从左到右(取决于语言环境，阿拉伯语就是从右到左)，reverse为true时，那么滑动方向就是从右往左。
    
    此属性本质上是决定可滚动widget的初始滚动位置是在“头”还是“尾”，取false时，初始滚动位置在“头”，反之则在“尾”，读者可以自己试验。
  */
  this.padding, 
  bool primary, 
  /*
    是否使用widget树中默认的 PrimaryScrollController；
    当滑动方向为垂直方向（scrollDirection值为Axis.vertical）并且controller没有指定时，primary默认为true.
  */
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
