### TextField 的构造函数及参数说明

``` dart
class TextField extends StatefulWidget {
  const TextField({
    Key key,
    this.controller,
    this.focusNode,
    this.decoration = const InputDecoration(),
    TextInputType keyboardType,
    this.textInputAction,
    this.textCapitalization = TextCapitalization.none,
    this.style,
    this.textAlign = TextAlign.start,
    this.textDirection,
    this.autofocus = false,
    this.obscureText = false,
    this.autocorrect = true,
    this.maxLines = 1,
    this.maxLength,
    this.maxLengthEnforced = true,
    this.onChanged,
    this.onEditingComplete,
    this.onSubmitted,
    this.inputFormatters,
    this.enabled,
    this.cursorWidth = 2.0,
    this.cursorRadius,
    this.cursorColor,
    this.keyboardAppearance,
    this.scrollPadding = const EdgeInsets.all(20.0),
    this.dragStartBehavior = DragStartBehavior.down,
    this.enableInteractiveSelection,
    this.onTap,
    this.buildCounter,
  }) : assert(textAlign != null),
       assert(autofocus != null),
       assert(obscureText != null),
       assert(autocorrect != null),
       assert(maxLengthEnforced != null),
       assert(scrollPadding != null),
       assert(dragStartBehavior != null),
       assert(maxLines == null || maxLines > 0),
       assert(maxLength == null || maxLength == TextField.noMaxLength || maxLength > 0),
       keyboardType = keyboardType ?? (maxLines == 1 ? TextInputType.text : TextInputType.multiline),
       super(key: key);
}
```

参数名字 | 参数类型 |	意义	| 必选 or 可选
- | - | - | -
key	| Key	| Widget 的标识	| 可选
controller	| TextEditingController	控制 TextField 的编辑，包括：设置/获取编辑框的内容、选择编辑内容、监听编辑文本改变事件，<br>如果没有设置，会有默认值（非常重要）	| 可选
focusNode	| FocusNode	| 用于控制TextField是否占有当前键盘的输入焦点,它是我们和键盘交互的一个handle（非常重要）	| 可选
decoration	| InputDecoration	| 用于控制TextField的外观显示，如提示文本、背景颜色、边框等（非常重要）	| 可选
textAlign	| TextAlign	| 文本的对齐方式	| 可选
textDirection	| TextDirection	| 文字方向	| 可选
keyboardType	| TextInputType	用于设置键盘类型	| 可选
textInputAction |	TextInputAction	| 键盘动作按钮图标(即回车键位图标)	| 可选
textCapitalization	| TextCapitalization	| 定义文本的大写格式	| 可选
style	| TextStyle	| 文本样式	| 可选
autofocus |	bool	| 是否自动获取焦点，默认为false |	可选
obscureText	| bool	| 是否隐藏正在编辑的文本，如用于输入密码的场景等，<br>文本内容会用“•”替换，默认为false	| 可选
autocorrect |	bool	| 单词自动校验，默认为true	| 可选
maxLines	| int	| 显示的最大行数，多行就是文本域	| 可选
maxLength	| int	| 允许输入的最大字符数	| 可选
maxLengthEnforced	| bool	| 是否强制限制最大字符数，默认为true，<br>true：强制限制最大字符数，<br>false：不限制最大字符数，即使设置了maxLength也不生效	|  | 可选
onChanged	| ValueChanged	| 输入框内容改变时的回调函数；<br>**注：内容改变事件也可以通过controller来监听**	| 可选
onEditingComplete	| VoidCallback	| 输入框输入完成时（也就是点击键盘的右下角时）触发，但是onEditingComplete没有参数，不会返回内容	| 可选
onSubmitted |	ValueChanged	| 输入框输入完成时触发，但是onSubmitted有参数，会返回内容	| 可选
inputFormatters	| List< TextInputFormatter> |	用于指定输入格式；当用户输入内容改变时，会根据指定的格式来校验。| 可选
enabled	| bool	| 输入框是否禁用，<br>如果为false，则输入框会被禁用，禁用状态不接收输入和事件，<br>同时显示禁用态样式（在其decoration中定义）。| 可选
cursorWidth	| double	| 自定义输入框光标宽度	| 可选
cursorRadius	| Radius	| 自定义输入框光标圆角	| 可选
cursorColor	| Color	| 自定义输入框光标颜色	| 可选
keyboardAppearance	| Brightness	| 设置键盘的亮度模式，只能在iOS上使用，有两种：Brightness.dart和Brightness.light	| 可选
scrollPadding	| EdgeInsets	| 文本框滑动时的间距	| 可选
dragStartBehavior |	DragStartBehavior	| 设置确定当用户启动拖动时拖动正式开始的时间	| 可选
enableInteractiveSelection |	bool	| 是否启用交互式选择true：长按将会选中文字，并且弹出 cut/copy/paste 的菜单	| 可选
onTap	| GestureTapCallback	| TextField的点击事件	| 可选
buildCounter	| InputCounterWidgetBuilder	| 生成自定义 InputDecorator.counter 小部件的回调	| 可选

### keyboardType：类型为TextInputType，用于设置该输入框默认的键盘输入类型

TextInputType的值	| 含义
- | - | -
TextInputType.text	| 文本输入键盘
TextInputType.multiline	| 多行文本，需和 maxLines 配合使用(设为null或大于1)
TextInputType.number	| 数字；会弹出数字键盘
TextInputType.phone	| 优化后的电话号码输入键盘；会弹出数字键盘并显示"* #"
TextInputType.datetime	| 优化后的日期输入键盘；Android上会显示“: -”
TextInputType.emailAddress	| 优化后的电子邮件地址；会显示“@ .”
TextInputType.url	| 优化后的url输入键盘； 会显示“/ .”

### [textInputAction](https://api.flutter.dev/flutter/services/TextInputAction-class.html)：类型为TextInputAction，键盘动作按钮图标(即回车键位图标)。

就是键盘右下角的那一个块图标。

textInputAction 的值 | 含义
- | - | -
TextInputAction.continueAction | continue（在安卓机上不支持）
TextInputAction.next | 下一步
TextInputAction.done | 完成
TextInputAction.newline | 换行
TextInputAction.go | 前往
TextInputAction.send | 发送

### [textCapitalization](https://api.flutter.dev/flutter/services/TextCapitalization-class.html)：类型为TextCapitalization，定义文本的大写格式。

TextCapitalization的值	| 含义
- | - | -
TextCapitalization.none	| 全部小写
TextCapitalization.characters	| 每个字符都大写
TextCapitalization.words	| 每个单词的首字母大写
TextCapitalization.sentences	| 每个句子的首字母大写

### 获取 TextField 内容

有两种方法：onChanged 的形参、controller.text

onChanged: 每当 TextField 内容改变，立即触发，唯一的函数形参就是文本框的值。
controller: TextField 的控制类（TextEditingController 的实例），可以控制 TextField 的编辑。

### 监听焦点状态

`FocusNode` 继承自 `ChangeNotifier`，通过 `FocusNode` 可以监听焦点的改变事件，代码如下：

```
FocusNode _focusNode = FocusNode();
_focusNode.addEventListener(() {
  // 获取焦点为 true，失去焦点为 false
  print(_focusNode.hasFocus);
});

TextField(
  focusNode: _focusNode
)
```

### 隐藏键盘

当点击空白区域或者键盘右下角的完成时，应该隐藏键盘。通过使当前的 TextField 失焦即可实现隐藏键盘：

```
void _onTapped(BuildContext context) {
  FocusScope.of(context).requestFocus(FocusNode());
  _nameFocusNode.unfocus();
}

GestureDetector(
  // 解决默认透明区域不响应事件的 bug（或者在祖先部件添加背景色）
  behavior: HitTestBehavior.translucent,
  onTap: () {
    _onTapped(context);
  },
  child: TextField(
    onEditingComplete: () {
      _onTapped(context);
    }
  )
)
```

### TextField 输入框长度如何不显示？

可能会通过 maxlength 属性限制 TextField 输入字符的长度，默认会在 TextField 右下部有计数的功能，可以通过设置：
- InputDecoration > counterText 为空字符串（更简单）
- InputDecoration > counterStyle字体颜色设置为 transparent

TextField 输入框长度如何不显示：
``` 
decoration: InputDecoration(
  counterText: ''
)

decoration: InputDecoration(
  counterStyle: TextStyle(
    color: Colors.transparent
  )
)
```

### 怎么把输入框放到 appbar 中并且 appbar 自适应高度和宽度


