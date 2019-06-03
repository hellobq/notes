### 单选按钮 Radio

`Radio` 是一个 Material 风格的单选按钮部件。

继承关系：
```
Object > Diagnosticable > DiagnosticableTree > Widget > StatefulWidget > Radio
```

由继承关系可知，类似 `Switch`，`Radio` 也是一个有状态的部件。

#### 构造函数

当 value == groupValue 时，则选中。

``` dart
Radio({
  Key key, 
  @required T value, // 单按钮的值
  @required T groupValue, // 当前按钮组的值
  @required ValueChanged<T> onChanged, // 用户选择该按钮的回调
  Color activeColor, // 被选择后的颜色
  MaterialTapTargetSize materialTapTargetSize // 点击目标的最小尺寸
})
```

### RadioListTile

一个 Radio 衍生的部件，给 Radio 带有标签 label 和图标 icon。`listTile + Radio`

- 整个列表图块都是交互式的，点击任何区域都能触发 Radio 的 onChanged 方法。
- 如果要禁用 RadioListTile，将 onChanged 赋值为 null 即可。

继承关系
```
Object > Diagnosticable > DiagnosticableTree > Widget > StatelessWidget > RadioListTile
```

#### RadioListTile 构造方法

``` dart
RadioListTile({
  Key key, 
  @required T value, 
  @required T groupValue, 
  @required ValueChanged<T> onChanged, 
  Color activeColor, 
  Widget title, 
  Widget subtitle, 
  bool isThreeLine: false, // 是否竖直排列为三行，无实际意义
  bool dense, //  是否密集垂直  设置为 true，文字会缩小
  Widget secondary, // 左边的控件，一般为 icon
  bool selected: false, 
  /*
    text 和 icon 的 color 是否是 activeColor 的颜色
      true：单选被选中时 text 和 icon 的颜色是 activeColor 的颜色
      false：单选被选中时 text 和 icon 不变色，仅单选按钮变色
  */
  ListTileControlAffinity controlAffinity: ListTileControlAffinity.platform
  /*
    Radio 控件相对于文本的位置。默认是根据平台
      ListTileControlAffinity.platform 根据不同的平台，来显示 对话框 的位置
      ListTileControlAffinity.leading ：勾选在左，title 在中，secondary 在右
      ListTileControlAffinity.trailing：勾选在右，title 在中，secondary 在左
  */
})
```

RadioListTile demo 如下：
```
import 'package:flutter/material.dart';

enum SingingCharacter {
  lafayette,
  jefferson
}

void main() => runApp(MyApp());

class MyApp extends StatelessWidget{
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Raised Button'),
        ),
        body: Container(
          child: MyRadio()
        )
      )
    );
  }
}

class MyRadio extends StatefulWidget {
  @override
  _MyRadioState createState() => _MyRadioState();
}

class _MyRadioState extends State<MyRadio> {
  SingingCharacter _character = SingingCharacter.lafayette;
  @override
  Widget build(BuildContext context) {
    return Container(
      child: Column(
        children: <Widget>[
          RadioListTile<SingingCharacter>(
            title: Text('Lafayette'),
            value: SingingCharacter.lafayette,
            groupValue: _character,
            onChanged: (SingingCharacter value) {
              setState(() {
                _character = value;
              });
            },
            secondary: Icon(
              Icons.add_alarm
            ),
          ),
          RadioListTile<SingingCharacter>(
            title: Text('Thomas Jefferson'),
            value: SingingCharacter.jefferson,
            groupValue: _character,
            onChanged: (SingingCharacter value) {
              setState(() { 
                _character = value; 
              });
            },
            subtitle: Text('subTitle'),
            secondary: Icon(
              Icons.add_alert
            ),
          ),
        ],
      )
    );
  }
}
```

### 相关连接：
- [flutter Radio](https://api.flutter.dev/flutter/material/Radio-class.html)
- [flutter RadioListTile](https://api.flutter.dev/flutter/material/RadioListTile-class.html)
