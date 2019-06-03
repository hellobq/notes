### 开关控件 Switch

Switch 是一个 Material 风格的、切换按钮的组件部件，通常用于设置的选项中。

继承关系：
```
Object > Diagnosticable > DiagnosticableTree > Widget > StatefulWidget > Switch
```

由继承关系可知，Switch 是一个有状态的部件，即它的状态 “value”。

#### Switch 构造函数

Switch 默认是创建一个 Material 风格的开关控件，也可以使用 Switch.adaptive 创建 IOS 风格下的实例。

``` dart
Switch({
  Key key, 
  @required bool value, // true：开 false：关
  @required ValueChanged<bool> onChanged, // 变化时回调
  Color activeColor, // 打开状态下 thumb(上面的圆点) 颜色
  Color activeTrackColor, // 打开状态下 track（下方的圆形矩形） 颜色
  Color inactiveThumbColor, // 关闭状态 thumb 颜色
  Color inactiveTrackColor, // 关闭状态 track 颜色
  ImageProvider activeThumbImage, // 打开状态下 thumb 图片
  ImageProvider inactiveThumbImage, // 关闭状态 thumb 图片
  MaterialTapTargetSize materialTapTargetSize, // 点击区域
  DragStartBehavior dragStartBehavior: DragStartBehavior.start 
})

Switch.adaptive({
  // 参数同上  
})
```

通过以上各种属性，可以自定义各种部件样式。

### SwitchListTile 

一个 Switch 衍生的部件，给 Switch 带有标签 label 和图标 icon。`listTile + Switch`

- 整个列表图块都是交互式的，点击任何区域都能触发 Switch 的 onChanged 方法。
- 如果要禁用 SwitchListTile，将 onChanged 赋值为 null 即可。

继承关系
```
Object > Diagnosticable > DiagnosticableTree > Widget > StatelessWidget > SwitchListTile
```

#### SwitchListTile 构造函数

SwitchListTile 默认是创建一个 Material 风格的开关控件，也可以使用 SwitchListTile.adaptive 创建 IOS 风格下的实例。

``` dart
SwitchListTile({
  Key key, 
  @required bool value, 
  @required ValueChanged<bool> onChanged, 
  Color activeColor, 
  Color activeTrackColor, 
  Color inactiveThumbColor, 
  Color inactiveTrackColor, 
  ImageProvider activeThumbImage, 
  ImageProvider inactiveThumbImage, 
  Widget title, 
  Widget subtitle, 
  bool isThreeLine: false, 
  bool dense, 
  Widget secondary, 
  bool selected: false 
})

SwitchListTile.adaptive({
  // 同上
})
```

### Switch、SwitchListTile demo 如下：

```
import 'package:flutter/material.dart';
import './MyIcon.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget{

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Raised Button'),
        ),
        body: SingleChildScrollView(
          child: Column(
            children: <Widget>[
              MySwitch(),
              MySwitchListTile()
            ],
          )
        )
      )
    );
  }
}

class MySwitch extends StatefulWidget {
  @override
  _MySwitchState createState() => _MySwitchState();
}

class _MySwitchState extends State<MySwitch> {
  bool value = false;
  @override
  Widget build(BuildContext context) {
    return Container(
      child: Switch(
        value: value,
        onChanged: (bool){
          print('switch 切换了 $bool');
          setState(() {
            value = bool;
          });
        }
      )
    );
  }
}

class MySwitchListTile extends StatefulWidget {
  @override
  _MySwitchListTileState createState() => _MySwitchListTileState();
}

class _MySwitchListTileState extends State<MySwitchListTile> {
  bool value = false;
  @override
  Widget build(BuildContext context) {
    return Container(
      child: SwitchListTile.adaptive(
        value: value,
        onChanged: (bool) {
          print('SwitchListTile changed $bool');
          setState(() {
            value = bool;
          });
        },
        secondary: Icon(
          Icons.android
        ),
        title: Text('title'),
        subtitle: Text('subTitle'),
      )
    );
  }
}
```
