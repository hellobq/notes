### 按钮 Button

Material widget 库中提供了多种按钮 Widget 如 RaisedButton、FlatButton、OutlineButton 等。它们有以下共同点：

- 选择性地继承 MaterialButton 类。
- 按下时都会有“水波动画”。
- 有一个onPressed属性来设置点击回调，当按钮按下时会执行该回调，**如果不提供该回调则按钮会处于禁用状态，禁用状态不响应用户点击**。
- 都有额外的命名构造函数 RaisedButton.icon/FlatButton.icon/OutlineButton.icon，来创建带有 icon、label 的相关 button。

### RaisedButton “突起/浮标”按钮

RaisedButton 它默认带有阴影和灰色背景。按下后，阴影会变大。

RaisedButton.icon 命名构造函数，来创建带有 icon、label 的 RaisedButton。

``` dart
(new) RaisedButton({
  Key key,  // Widget 的标识
  Widget child, // 按钮的内容
  @required () → void onPressed, // 按钮点击后的回调，如果不设置，该按钮就被禁用
  (bool) → void onHighlightChanged,  // 水波纹高亮变化回调，按下返回true，抬起返回false
  ButtonTextTheme textTheme, // 按钮的主题
  Color textColor, // 文字的颜色
  Color disabledTextColor, // 按钮禁用时候文字的颜色
  Color color, // 按钮的背景颜色
  Color disabledColor, // 按钮禁用时候文字的颜色
  Color highlightColor, // 按钮高亮色，也就是水波纹下面的颜色
  Color splashColor, // 水波纹的颜色
  Brightness colorBrightness, // 按钮主题高亮/不高亮(light/dark)
  double elevation, // 按钮下面的阴影
  double highlightElevation, // 按钮高亮时的阴影
  double disabledElevation, // 按钮按下的阴影
  EdgeInsetsGeometry padding, // 按钮内填充，可通过其设置按钮高度
  ShapeBorder shape, // 设置外形
  Clip clipBehavior: Clip.none, //根据此选项，内容将被剪裁（或不剪辑）
  MaterialTapTargetSize materialTapTargetSize, //配置点击目标的最小尺寸
  Duration animationDuration //定义形状和高程的动画更改的持续时间
}) → RaisedButton

(new) RaisedButton.icon({
  ...
  @required Widget icon, 
  @required Widget label
}) → RaisedButton
```

RaisedButton demo 如下：

```
import 'package:flutter/material.dart';

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
              RaisedButton(
                onPressed: (){},//设置是否禁用、或启用控件
                child: Text('Disabled Button'),
              ),
              RaisedButton(
                onPressed: null,//设置是否禁用、或启用控件
                child: const Text('Disabled Button '),
              ),
              RaisedButton(
                onPressed: () {},
                child: const Text('Enabled Button'),
              ),
              RaisedButton(
                onPressed: () {},
                child: Text("textColor文本的颜色，color背景颜色，highlightColor按钮按下的颜色"),
                textColor: Color(0xffff0000),
                color: Color(0xff11f1f1),
                highlightColor: Color(0xff00ff00),
                padding: EdgeInsets.all(10.0)
              ),
              RaisedButton(
                onPressed: null,
                child: Text("disabledTextColor禁用时文本颜色，disabledColor禁用时背景颜色"),
                disabledTextColor: Color(0xff999999),
                disabledColor: Color(0xffff0000),
              ),
              RaisedButton(
                onPressed: () {},
                child: Text("splashColor水波的颜色"),
                splashColor: Color(0xffff0000),
              ),
              RaisedButton(
                onPressed: () {},
                child: Text("colorBrightness按钮主题高亮 Brightness.light"),
                colorBrightness: Brightness.light,
              ),
              RaisedButton(
                onPressed: () {},
                child: Text("colorBrightness按钮主题高亮 Brightness.dark"),
                colorBrightness: Brightness.dark,
              ),
              RaisedButton(
                onPressed: () {},
                child: Text("elevation按钮下面的阴影,"),
                elevation: 15.0,
              ),
              RaisedButton(
                onPressed: () {},
                child: Text("highlightElevation高亮时候的阴影"),
                highlightElevation: 5,
              ),
              RaisedButton(
                onPressed: () {},
                child: Text("disabledElevation按下的时候的阴影"),
                disabledElevation: 50.0,
              ),
              RaisedButton(
                onPressed: () {
                  print("RaisedButton== onPressed");
                },
                child: Text("onHighlightChanged 水波纹高亮变化回调,按下返回true,抬起返回false"),
                onHighlightChanged: (bool b) {
                  print("RaisedButton== $b");
                },
              ),
              RaisedButton(
                onPressed: () {
                  print("点击了");
                },
                child: Text("onPressed点击事件"),
              ),
              RaisedButton(
                onPressed: () {},
                child: Text("配置点击目标的最小尺寸"),
                materialTapTargetSize: MaterialTapTargetSize.shrinkWrap,
              ),
              RaisedButton(
                onPressed: () {},
                child: Text("定义形状和高程的动画更改的持续时间"),
                animationDuration: Duration(hours: 1),
              ),
              RaisedButton(
                onPressed: () {},
                textColor: Colors.white,
                padding: const EdgeInsets.all(0.0),
                child: Container(
                  decoration: const BoxDecoration(
                    gradient: LinearGradient(
                      colors: <Color>[Colors.red, Colors.green, Colors.blue],
                    ),
                  ),
                  padding: const EdgeInsets.all(10.0),
                  child: Text('Gradient Button'),
                ),
              ),
              RaisedButton.icon(
                icon: Icon(
                  Icons.add
                ),
                label: Text('增加'),
                onPressed: () {}
              ),
              RaisedButton.icon(
                onPressed: () {},
                // 设置圆角
                shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(20.0)),
                icon: Container(
                  width: 20.0,
                  height: 20.0,
                  alignment: Alignment(0.0, 0.0),
                  decoration: BoxDecoration(
                    borderRadius: BorderRadius.all(Radius.circular(10.0)),
                    color: Colors.black26
                  ),
                  child: Icon(
                    Icons.add,
                    size: 20.0
                  )
                ),
                label: Text('增加')
              )
            ],
          )
        )
      )
    );
  }
}
```

### OutlineButton 边框按钮

OutlineButton 默认有一个边框，背景透明且不带阴影。当按下后，边框颜色会变亮，同时会有背景和较弱的阴影。

OutlineButton.icon 命名构造函数用来创建带有 icon、label 的 OutlineButton。

``` dart
OutlineButton({
  Key key, 
  @required VoidCallback onPressed, 
  ButtonTextTheme textTheme, 
  Color textColor, 
  Color disabledTextColor, 
  Color color, 
  Color highlightColor, 
  Color splashColor, 
  double highlightElevation, 
  BorderSide borderSide, 
  Color disabledBorderColor, 
  Color highlightedBorderColor, 
  EdgeInsetsGeometry padding, 
  ShapeBorder shape, 
  Clip clipBehavior: Clip.none, 
  Widget child 
})

OutlineButton.icon({
  // ...
  @required Widget icon,
  @required Widget label
})
```

OutlineButton demo 如下：

```
SingleChildScrollView(
  child: Column(
    children: <Widget>[
      OutlineButton(
        onPressed: () {},
        child: Text('默认按钮')
      ),
      OutlineButton.icon(
        onPressed: () {},
        icon: Icon(
          Icons.message,
          size: 20.0,
          color: Colors.indigo,
        ),
        label: Text('发送信息')
      )
    ],
  )
)
```

### FlatButton 扁平按钮

FlatButton 默认背景透明且不带阴影。当按下后，会有背景色。

类似 RaisedButton，FlatButton.icon 命名构造函数用来创建带有 icon、label 的 FlatButton。

``` dart
FlatButton({
  Key key,
  @required Widget child, 
  @required VoidCallback onPressed, 
  ValueChanged<bool> onHighlightChanged, 
  ButtonTextTheme textTheme, 
  Color textColor, 
  Color disabledTextColor, 
  Color color, 
  Color disabledColor, 
  Color highlightColor, 
  Color splashColor, 
  Brightness colorBrightness, 
  EdgeInsetsGeometry padding, 
  ShapeBorder shape, 
  Clip clipBehavior: Clip.none, 
  MaterialTapTargetSize materialTapTargetSize
})

FlatButton.icon({
  // ...
  @required Widget icon,
  @required Widget label
})
```

FlatButton demo 如下：

```
SingleChildScrollView(
  child: Column(
    children: <Widget>[
      FlatButton(
        onPressed: () {},
        child: Text('默认按钮')
      ),
      FlatButton.icon(
        onPressed: () {},
        icon: Icon(
          Icons.message,
          size: 20.0,
          color: Colors.indigo,
        ),
        label: Text('发送信息')
      )
    ],
  )
)
```

### IconButton 仅包含 icon 的 button

IconButton 致力于创建一个可点击的 button，仅有 icon，不包括文字，默认没有背景，点击后出现背景。

``` dart
IconButton({
  Key key, 
  double iconSize: 24.0, 
  EdgeInsetsGeometry padding: const EdgeInsets.all(8.0), 
  AlignmentGeometry alignment: Alignment.center, 
  @required Widget icon, 
  Color color, 
  Color highlightColor, 
  Color splashColor, 
  Color disabledColor, 
  @required VoidCallback onPressed, 
  String tooltip // 长按出提示文字（有延迟）
})
```

IconButton demo 如下：

```
IconButton(
  icon: Icon(
    Icons.mode_edit
  ),
  onPressed: () {},
  tooltip: '编辑内容',
)
```

### RawMaterialButton 创建自定义 button

``` dart
RawMaterialButton({
  Key key,  
  Widget child,
  @required VoidCallback onPressed, 
  ValueChanged<bool> onHighlightChanged, 
  TextStyle textStyle, 
  Color fillColor, 
  Color highlightColor, 
  Color splashColor, 
  double elevation: 2.0, 
  double highlightElevation: 8.0, 
  double disabledElevation: 0.0, 
  EdgeInsetsGeometry padding: EdgeInsets.zero, 
  BoxConstraints constraints: const BoxConstraints(minWidth: 88.0, minHeight: 36.0), 
  ShapeBorder shape: const RoundedRectangleBorder(), 
  Duration animationDuration: kThemeChangeDuration, 
  Clip clipBehavior: Clip.none, 
  MaterialTapTargetSize materialTapTargetSize
})
```

RawMaterailButton demo 如下：

```
RawMaterialButton(
  constraints: BoxConstraints.tight(Size(36, 36)),
  onPressed: () {},
  child: Icon(
    Icons.trending_up, 
    size: 18
  ),
  shape: CircleBorder(),
  elevation: 0.0,
  fillColor: Color.fromARGB(255, 240, 240, 240),
)
```


### 相关连接：

- [flutter RaisedButton](https://api.flutter.dev/flutter/material/RaisedButton-class.html)
- [flutter FlatButton](https://api.flutter.dev/flutter/material/FlatButton-class.html)
- [flutter OutlineButton](https://api.flutter.dev/flutter/material/OutlineButton-class.html)
- [flutter IconButton](https://api.flutter.dev/flutter/material/IconButton-class.html)
- [flutter RawMaterialButton](https://api.flutter.dev/flutter/material/RawMaterialButton-class.html)
