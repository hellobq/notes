### ScrollController 

用户监听滚动部件的滚动情况（获取滚动位置），控制滚动。

ScrollController 的构造函数如下：

``` dart
ScrollController({
  double initialScrollOffset = 0.0, //初始滚动位置
  this.keepScrollOffset = true, //是否保存滚动位置
  ...
})
```

ScrollController 的属性和方法：
- offset：获取可滚动 widget 的滚动位置。
- jumpTo(double offset)、animateTo(double offset,...)：这两个方法用于跳转到指定的位置，它们不同之处在于，后者在跳转时会执行一个动画，而前者不会。

实现滚动的监听：
``` dart
ScrollController _scrollController = ScrollController();
_scrollController.addListener(() {
  print(_scrollController.offset);

  // 滚动到底
  if (_scrollController.position.pixels == _scrollController.position.maxScrollExtent) {
    ....
  }
})
```

offset 实际上就是 position.pixels 的便捷方式：
``` dart
double get offset => position.pixels;
```

### NotificationListener

NotificationListener 是一个 Widget，模板参数T是想监听的通知类型，
- 如果省略，则所有类型通知都会被监听，
- 如果指定特定类型，则只有该类型的通知会被监听。
- NotificationListener 需要一个 onNotification 回调函数，用于实现监听处理逻辑，该回调可以返回一个布尔值，代表是否阻止该事件继续向上冒泡。

``` dart
// 监听 ListView 的滚动通知，然后显示当前滚动进度百分比
import 'package:flutter/material.dart';

class ScrollNotificationTestRoute extends StatefulWidget {
  @override
  _ScrollNotificationTestRouteState createState() => _ScrollNotificationTestRouteState();
}

class _ScrollNotificationTestRouteState
    extends State<ScrollNotificationTestRoute> {
  String _progress = "0%";

  @override
  Widget build(BuildContext context) {
    return Scrollbar(
      child: NotificationListener<ScrollNotification>(
        onNotification: (ScrollNotification notification) {
          double progress = notification.metrics.pixels / notification.metrics.maxScrollExtent;
          setState(() {
            _progress = "${(progress * 100).toInt()}%";
          });
          print("BottomEdge: ${notification.metrics.extentAfter == 0}");
          //return true; //放开此行注释后，进度条将失效
        },
        child: Stack(
          alignment: Alignment.center,
          children: <Widget>[
            ListView.builder(
              itemCount: 100,
              itemExtent: 50.0,
              itemBuilder: (context, index) => ListTile(title: Text("$index"))
            ),
            CircleAvatar(  //显示进度百分比
              radius: 30.0,
              child: Text(_progress),
              backgroundColor: Colors.black54,
            )
          ],
        ),
      ),
    );
  }
}
```
