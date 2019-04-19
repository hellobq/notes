# Column 布局

竖向布局: 依靠 Column 组件实现，它有多个配置选项(Row 组件也有的)：

主轴 mainAxisAlignment: 
- MainAxisAlignment.start
- MainAxisAlignment.center
- MainAxisAlignment.end

副轴 crossAxisAlignment 对其属性
- CrossAxisAlignment.star：居左对齐。
- CrossAxisAlignment.center：居中对齐。
- CrossAxisAlignment.end：居右对齐。


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
          title: Text("Column"),
        ),
        body: Center(
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.center,
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              Text('let the crowd follow you.'),
              Expanded(  // 中间灵活布局
                child: Text('The code word is ‘Rochambeau,’ dig me?')
              ),
              Text('Rochambeau!'),
            ],
          )
        )
      ),
    );
  }
}
```
