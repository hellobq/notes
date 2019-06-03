### 复选按钮 Checkbox

创建一个 Material 风格的复选框。

- 复选框本身不保持任何状态。
- 当复选框的状态发生变化时，窗口小部件回调用 `onChanged` 回调。
- 大多数使用复选框的小部件将侦听onChanged回调并使用新值重建复选框以更新复选框的可视外观。

继承关系
```
Object > Diagnosticable > DiagnosticableTree > Widget > StatefulWidget > Checkbox
```

#### Checkbox 构造函数

``` dart
Checkbox({
  Key key, 
  @required bool value, // 是否选中此复选框。
  bool tristate: false, // 如果为true，则复选框的值可以为true，false或null。
  @required ValueChanged<bool> onChanged, // 当复选框的值更改时调用
  Color activeColor, // 复选框被选中时的颜色（背景色）
  Color checkColor, // 选中此复选框时用于检查图标的颜色（√的颜色）
  MaterialTapTargetSize materialTapTargetSize // 配置点击目标的最小尺寸
})
```

Checkbox demo 如下：
```
Checkbox(
  value: _value1,
  onChanged: (bool) {
    print('被点击 $bool');
    setState(() {
      _value1 = bool;
    });
  },
  activeColor: Colors.red,
  checkColor: Colors.green,
),
Checkbox(
  value: _value2,
  onChanged: (bool) {
    print('被点击 $bool');
    setState(() {
      _value2 = bool;
    });
  },
  activeColor: Colors.red,
)
```

### CheckboxListTile 

一个 Checkbox 衍生的部件，给 Checkbox 带有标签 label 和图标 icon。`listTile + Checkbox`

- 整个列表图块都是交互式的，点击任何区域都能触发 Checkbox 的 onChanged 方法。
- 如果要禁用 CheckboxListTile，将 onChanged 赋值为 null 即可。

继承关系
```
Object > Diagnosticable > DiagnosticableTree > Widget > StatelessWidget > CheckboxListTile
```

#### CheckboxListTile 构造函数

和 [RadioListTile](单选按钮 Radio.md) 构造函数参数大同小异，仅是泛型具体化为 bool。

``` dart
CheckboxListTile({
  Key key, 
  @required bool value, 
  @required ValueChanged<bool> onChanged, 
  Color activeColor, 
  Widget title, 
  Widget subtitle, 
  bool isThreeLine: false, 
  bool dense, 
  Widget secondary, 
  bool selected: false, 
  ListTileControlAffinity controlAffinity: ListTileControlAffinity.platform 
})
```

CheckboxListTile demo 如下：
```
child: Column(
  children: <Widget>[
    CheckboxListTile(
      title: Text('Android'),
      value: _value1,
      onChanged: (bool) {
        setState(() {
          _value1 = bool;
        });
      },
      secondary: Icon(
        Icons.android
      ),
    ),
    CheckboxListTile(
      title: Text('Alarm'),
      value: _value2,
      onChanged: (bool) {
        setState(() {
          _value2 = bool;
        });
      },
      selected: true,
      secondary: Icon(
        Icons.add_alarm
      ),
    )
  ],
)
```
