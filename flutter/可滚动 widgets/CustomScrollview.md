### CustomScrollview 子定义滚动 widget

CustomScrollview 的子部件必须是 `slivers`，通过 Sliver 可实现多个可滚动视图的组合。CustomScrollView 构造函数定义如下：

``` dart
CustomScrollView({
  Key key, 
  Axis scrollDirection: Axis.vertical, 
  bool reverse: false, 
  ScrollController controller, 
  bool primary, 
  ScrollPhysics physics, 
  bool shrinkWrap: false, 
  Key center, 
  double anchor: 0.0, 
  double cacheExtent, 
  List<Widget> slivers: const <Widget> [], 
  /*
    包含 slivers 家族：SliverAppBar、SliverList、SliverGrid、SliverPersidentHeader、SliverToBoxAdapter
  */
  int semanticChildCount, 
  DragStartBehavior dragStartBehavior: DragStartBehavior.down
}
```

### SliverAppBar 

SliverAppBar 来实现 AppBar 展开和收起功能。SliverAppBar 的构造函数定义如下：

``` dart
SliverAppBar({
  ...
  Widget leading, 
  bool automaticallyImplyLeading: true, 
  Widget title, 
  List<Widget> actions, 
  Widget flexibleSpace, 
  PreferredSizeWidget bottom, 
  double elevation, 
  bool forceElevated: false, 
  Color backgroundColor, 
  Brightness brightness, 
  IconThemeData iconTheme, 
  TextTheme textTheme, 
  bool primary: true, 
  bool centerTitle, 
  double titleSpacing: NavigationToolbar.kMiddleSpacing, 

  double expandedHeight, 
  bool floating: false, 
  /*
    ListView 并没有到达顶部，是否展开 AppBar:
      设置为 true，下滑 ListView 时，即使 ListView 并没有到达顶部 AppBar 也会立即展开
  */
  bool pinned: false, 
  /*
    控制 ListView 上滑时，AppBar 是否出现。默认：上滑 ListView，不显示 AppBar
  */
  bool snap: false
  /*
    控制是否显示 flexibleSpace
  */
})

AppBar({
  ...
  Widget leading, 
  bool automaticallyImplyLeading: true, 
  Widget title, 
  List<Widget> actions, 
  Widget flexibleSpace, 
  PreferredSizeWidget bottom,
  double elevation, 
  Color backgroundColor, 
  Brightness brightness, 
  IconThemeData iconTheme, 
  TextTheme textTheme, 
  bool primary: true, 
  bool centerTitle, 
  double titleSpacing: NavigationToolbar.kMiddleSpacing, 

  double toolbarOpacity: 1.0, 
  double bottomOpacity: 1.0
})
```

由 SliverAppBar 和 AppBar 部件构造函数可知，两者构造函数所需参数大致相同。给 SliverAppBar 设置 flexibleSpace 和 expandedHeight 属性，就可以轻松完成AppBar展开/收起的功能。

``` dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget{

  @override
  Widget build(BuildContext context) {
    String str = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

    return MaterialApp(
      home: Scaffold(
        body: CustomScrollView(
          slivers: <Widget>[
            SliverAppBar(
              title: Text('SliverAppBar'),
              backgroundColor: Theme.of(context).accentColor,
              expandedHeight: 200.0,
              flexibleSpace: FlexibleSpaceBar(
                background: Image.asset('images/avatar.jpg', fit: BoxFit.cover),
              ),
              floating: true,
              snap: true,
              pinned: false,
            ),
            SliverList(
              delegate: SliverChildListDelegate(
                str.split('')
                  .map((c) => Text(c, textScaleFactor: 2.0, textAlign: TextAlign.center,))
                  .toList()
              ),
            ),
          ]
        )
      ),
    );
  }
}
```

### SliverList

只需设置 `delegate` 属性即可，一般使用 `SliverChildBuilderDelegate / SliverChildListDelegate`。

使用 SliverChildBuilderDelegate 时，需要设置 childCount，否则 Flutter 不知道怎么绘制：

``` dart
SliverList(
  delegate: SliverChildBuilderDelegate(
    (context, idx) => Text(str[idx], textScaleFactor: 2.0, textAlign: TextAlign.center),
    childCount: str.length
  ),
),

SliverList(
  delegate: SliverChildListDelegate(
    str.split('')
      .map((c) => Text(c, textScaleFactor: 2.0, textAlign: TextAlign.center,))
      .toList()
  ),
),
```

两者区别：
- SliverChildBuilderDelegate 用于动态绘制，类似 ListView.builder
- SliverChildListDelegate 用于数量明确的列表（不应超过一屏），不适合多数量，效率上有问题。

### SliverFixedExtentList

在 SliverList 基础上添加 `itemExtent`，来规定子部件在主轴方向上的长度。

### SliverGrid

同 GridView，SliverGrid 的表现也与之类似，也有类似的构造函数：SliverGrid、SliverGrid.count, SliverGrid.extend。

``` dart
SliverGrid.count({
  ...
  int crossAxisCount, 
  /*
    负轴上的数目
  */
  double mainAxisSpacing: 0.0, 
  /*
    每一行 item 的主轴间距
  */
  double crossAxisSpacing: 0.0, 
  /*
    负轴上的间距
  */
  double childAspectRatio: 1.0, 
  /*
    宽 / 长的比例
  */
  List<Widget> children: const <Widget> []
})

SliverGrid.extent({
  ...
  double maxCrossAxisExtent, 
  double mainAxisSpacing: 0.0, 
  double crossAxisSpacing: 0.0, 
  double childAspectRatio: 1.0, 
  List<Widget> children: const <Widget> []
})
```

可见 SliverGrid 构造函数参数比 GridView 相比：少了些属性

### SliverPadding

为 slivers 提供内边距，SliverPadding 的构造函数、demo 如下：

``` dart
SliverPadding({
  ...
  EdgeInsetsGeometry padding, 
  Widget sliver
})

SliverPadding(
  padding: EdgeInsets.all(10.0),
  sliver: SliverGrid.extent(
    maxCrossAxisExtent: 100.0,
    crossAxisSpacing: 20.0,
    mainAxisSpacing: 10.0,
    children: <Widget>[
      Icon(Icons.ac_unit),
      Icon(Icons.airport_shuttle),
      Icon(Icons.all_inclusive),
      Icon(Icons.beach_access),
      Icon(Icons.cake),
      Icon(Icons.free_breakfast),
    ],
  )
),
```

### 相关链接
- [flutter 实战 CustomScrollView](https://book.flutterchina.club/chapter6/custom_scrollview.html)
- [slivers 滚动组合](https://juejin.im/post/5bceb534e51d457aa4596f9a#heading-4)
