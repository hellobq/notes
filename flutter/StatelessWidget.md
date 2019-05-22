# StatelessWidget

无状态部件。用于创建无状态 widget。StatelessWidget 标识该组件只会渲染一次。所需数据是 `外界通过构造函数传进来的`。

只有从外界传过来的数据源发生变化，就会重新 build（也仅有这个一个声明周期）。

``` dart
import 'package:flutter/material.dart';

class MyApp extends StatelessWidget {

  final String content;
  MyApp(this.content);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('StatelessWidget demo')
      ),
      body: Center(
        child: content.length != 0 ? Text(content) : null
      )
    );
  }
}
```
