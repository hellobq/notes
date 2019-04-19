# Row 布局

横向布局：灵活布局，非灵活布局

### 非灵活布局：如果子元素不足，则会留有空隙；如果子元素大小超出，则会警告。

``` dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: "GridView",
      home: Scaffold(
        appBar: AppBar(
          title: Text("GridView Widget"),
        ),
        body: Row(
          children: <Widget>[
            new RaisedButton(
              onPressed: (){},
              color: Colors.red,
              child: new Text('red btn')
            ),
            new RaisedButton(
              onPressed: (){},
              color: Colors.blue,
              child: new Text('blue btn')
            ),
            new RaisedButton(
              onPressed: (){},
              color: Colors.pink,
              child: new Text('pink btn')
            ),
            new RaisedButton(
              onPressed: (){},
              color: Colors.red,
              child: new Text('red btn')
            )
          ],
        ),
      ),
    );
  }
}
```

### 灵活布局：根据子元素的大小进行布局的。使用 `Expanded()` 实现。

``` dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: "GridView",
      home: Scaffold(
        appBar: AppBar(
          title: Text("GridView Widget"),
        ),
        body: Row(
          children: <Widget>[
            Expanded(
              child: new RaisedButton(
                onPressed: (){},
                color: Colors.red,
                child: new Text('red btn')
              )
            ),
            Expanded(
              child: new RaisedButton(
                onPressed: (){},
                color: Colors.blue,
                child: new Text('blue btn')
              )
            ),
            Expanded(
              child: new RaisedButton(
                onPressed: (){},
                color: Colors.pink,
                child: new Text('pink btn')
              )
            ),
            Expanded(
              child: new RaisedButton(
                onPressed: (){},
                color: Colors.red,
                child: new Text('red btn')
              )
            ),
            Expanded(
              child: new RaisedButton(
                onPressed: (){},
                color: Colors.red,
                child: new Text('red btn')
              )
            )
          ],
        ),
      ),
    );
  }
}
```

### 非灵活布局和灵活布局混合使用

现在Row Widget里有3个按钮，实现两边的按钮保持原大小，中间的按钮填充剩余空间，使它们占满一行不留空隙。

直接去掉 `Expanded()` 即可

``` dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: "GridView",
      home: Scaffold(
        appBar: AppBar(
          title: Text("GridView Widget"),
        ),
        body: Row(
          children: <Widget>[
            new RaisedButton(   // 不灵活
              onPressed: (){},
              color: Colors.red,
              child: new Text('red btn')
            ),
            Expanded(
              child: new RaisedButton(
                onPressed: (){},
                color: Colors.blue,
                child: new Text('blue btn')
              )
            ),
            Expanded(
              child: new RaisedButton(
                onPressed: (){},
                color: Colors.pink,
                child: new Text('pink btn')
              )
            ),
            new RaisedButton(   // 不灵活
              onPressed: (){},
              color: Colors.red,
              child: new Text('red btn')
            )
          ],
        ),
      ),
    );
  }
}
```
