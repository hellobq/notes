### Row、Column 线性布局

横向/竖直布局均包括：灵活布局，非灵活布局

继承关系：
```
Object > Diagnosticable > DiagnosticableTree > Widget > RenderObjectWidget > MultiChildRenderObjectWidget > Flex > Row/Column
```

由继承关系可知，Row/Column 均继承 `Flex`，实际运用中直接使用 Row/Column 即可。

Row 构造函数：
``` dart
Row({
  MainAxisAlignment mainAxisAlignment = MainAxisAlignment.start,
  /*
    主轴方向上子部件对齐方式：
      MainAxisAlignment.start 主轴起点
      MainAxisAlignment.center 中间对齐
      MainAxisAlignment.end 主轴终点
      MainAxisAlignment.spaceBetween 将主轴方向上的空白区域均分，使得children之间的空白区域相等，首尾child都靠近首尾，没有间隙
      MainAxisAlignment.spaceAround：将主轴方向上的空白区域均分，使得children之间的空白区域相等，但是首尾child的空白区域为1/2
      MainAxisAlignment.spaceEvenly：将主轴方向上的空白区域均分，使得children之间的空白区域相等，包括首尾child
  */
  CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center,
  /*
    CrossAxisAlignment.start：children在负轴上起点处展示
    CrossAxisAlignment.center：children在负轴上居中展示
    CrossAxisAlignment.end：children在负轴上末尾展示
    CrossAxisAlignment.baseline：在负轴方向，使得children的baseline对齐
    CrossAxisAlignment.stretch：让children填满负轴方向
  */
  List<Widget> children = const <Widget>[],

  MainAxisSize mainAxisSize = MainAxisSize.max,
  /*
    MainAxisSize.max：根据传入的布局约束条件，最大化主轴方向的可用空间
    MainAxisSize.min：与max相反，是最小化主轴方向的可用空间
  */
  Key key,
  TextDirection textDirection,
  VerticalDirection verticalDirection = VerticalDirection.down,
  TextBaseline textBaseline,
}
```

### 非灵活布局

如果子元素不足，则会留有空隙；如果子元素大小超出，则会警告。

``` dart
Row(
  children: <Widget>[
    RaisedButton(
      onPressed: (){},
      color: Colors.red,
      child: Text('red btn')
    ),
    RaisedButton(
      onPressed: (){},
      color: Colors.blue,
      child: Text('blue btn')
    ),
    RaisedButton(
      onPressed: (){},
      color: Colors.pink,
      child: Text('pink btn')
    ),
    RaisedButton(
      onPressed: (){},
      color: Colors.red,
      child: Text('red btn')
    )
  ],
)
```

### 灵活布局

在 Row/Column 中，不确定的子部件宽度则使用 `Expanded()` 扩展宽度，并且对于剩余空间的扩展比例可以使用 `flex` 属性来指定。

``` dart
Row(
  children: <Widget>[
    Expanded(
      child: RaisedButton(
        onPressed: (){},
        color: Colors.red,
        child: Text('red btn')
      ),
      flex: 2
    ),
    Expanded(
      child: RaisedButton(
        onPressed: (){},
        color: Colors.blue,
        child: Text('blue btn')
      )
    ),
    Expanded(
      child: RaisedButton(
        onPressed: (){},
        color: Colors.pink,
        child: Text('pink btn')
      )
    ),
    Expanded(
      child: RaisedButton(
        onPressed: (){},
        color: Colors.red,
        child: Text('red btn')
      ),
      flex: 3
    ),
    Expanded(
      child: RaisedButton(
        onPressed: (){},
        color: Colors.red,
        child: Text('red btn')
      )
    )
  ],
)
```

### 非灵活布局和灵活布局混合使用

现在Row Widget里有3个按钮，实现两边的按钮保持原大小，中间的按钮填充剩余空间，使它们占满一行不留空隙。

``` dart
Row(
  children: <Widget>[
    RaisedButton( // 不灵活
      onPressed: (){},
      color: Colors.red,
      child: Text('red btn')
    ),
    Expanded(
      child: RaisedButton(
        onPressed: (){},
        color: Colors.blue,
        child: Text('blue btn')
      ),
      flex: 2  // 战剩余空间 2/3
    ),
    Expanded(
      child: RaisedButton(
        onPressed: (){},
        color: Colors.pink,
        child: Text('pink btn')
      )
    ),
    RaisedButton(   // 不灵活
      onPressed: (){},
      color: Colors.red,
      child: Text('red btn')
    )
  ],
)
```

### 相关链接
- [flutter Row](https://api.flutter.dev/flutter/widgets/Row-class.html)
- [flutter Column](https://api.flutter.dev/flutter/widgets/Column-class.html)
- [flutter Flex](https://api.flutter.dev/flutter/widgets/Flex-class.html)
- [flutter 实战 Row、Column](https://book.flutterchina.club/chapter4/row_and_column.html)
- [flutter 实战 Flex](https://book.flutterchina.club/chapter4/flex.html)
