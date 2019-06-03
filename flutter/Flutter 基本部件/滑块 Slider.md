### 滑块 Slider

`Slider` 是一个 Material 风格的滑块部件，用来选择范围性的数据（可以是连续的或者不连续的）。

默认是在一段最大值最小值间做任意值地选择，如果想选择间隔性的值，例如[0.0, 50.0]，选择10、15....50.0这样的值，给 divisions 设定一个非空整数5即可。

继承关系：
```
Object > Diagnosticable > DiagnosticableTree > Widget > StatefulWidget > Slider
```

关于 `Slider` 有以下术语：
- `thumb` 滑块，用户可以水平拖动移动的区域
- `track` 滑轨，thumb 可以滑动的线条区域
- `value indicator` 值指示器，当用户拖拽 thumb 时，显示当前所选的属性值
- `active` 选中区
- `inactive` 非选中区

#### 继承关系

```
Object > Diagnosticable > DiagnosticableTree > Widget > StatefulWidget > Slider
```
由继承关系，Slider 需要维护一个**滑动值**这个状态。

#### Slider 构造函数

``` dart
Slider({
  Key key, 
  @required double value, // 控件的位置
  @required ValueChanged<double> onChanged, // 如果为 null，将禁用滑块
  ValueChanged<double> onChangeStart, // 滑块初始事件
  ValueChanged<double> onChangeEnd, // 滑块结束事件
  double min: 0.0, // 最小值
  double max: 1.0, // 最大值
  int divisions, // 离散分区的数量
  String label, // 设置 divisions 时（必要），显示节点的 label
  Color activeColor, // 滑块轨道的活动部分的颜色
  Color inactiveColor, // 滑块轨道的非活动部分的颜色
  SemanticFormatterCallback semanticFormatterCallback 
})
```

如果当前 Slider 无法满足需求，可以通过 `SliderTheme` 定制复杂的样式。

#### Slide、SliderTheme demo 如下：

```
Slider(
  value: _value,
  min: 0.0,
  max: 100.0,
  divisions: 100,
  label: 'value: ${_value.toStringAsFixed(2)}',
  onChanged: (currentValue) {
    print('currentValue: $currentValue');
    setState(() {
      _value = currentValue;
    });
  },
  onChangeStart: (currentValue) {
    print('currentValue start: $currentValue');
    setState(() {
      _value = currentValue;
    });
  },
  onChangeEnd: (currentValue) {
    print('currentValue end: $currentValue');
    setState(() {
      _value = currentValue;
    });
  },
),
SliderTheme(
  data: SliderTheme.of(context).copyWith(
    // 滑轨颜色
    activeTrackColor: Colors.green,
    inactiveTrackColor: Colors.greenAccent,

    //提示进度气泡
    valueIndicatorColor: Colors.green,
    valueIndicatorTextStyle: TextStyle(
      color: Colors.white,
      fontWeight: FontWeight.w500
    ),

    // 滑块中心、滑块边缘
    thumbColor: Colors.red,
    overlayColor: Colors.redAccent,

    // divisions对进度线分割后，断续线中间间隔的颜色
    inactiveTickMarkColor: Colors.white,

  ),
  child: Slider(
    value: value,
    label: '$value',
    min: 0.0,
    max: 100.0,
    divisions: 10,
    onChanged: (val){
      setState(() {
        value = val.floorToDouble();//转化成double
      });
    }
  )
)
```

**注意**：当不设置 divisions 时，即使设置了 label，也不会显示，此时只要将 divisions 值设置为 max 值即可。

### 相关链接：
- [Flutter Slider don't show label](https://stackoverflow.com/questions/55233504/flutter-slider-doesnt-show-label)
- [Flutter Slider](https://api.flutter.dev/flutter/material/Slider-class.html)
- [Flutter SliderTheme](https://api.flutter.dev/flutter/material/SliderTheme-class.html)
