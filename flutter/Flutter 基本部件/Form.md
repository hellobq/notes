### Form 表单的构造函数及参数说明

``` dart
class Form extends StatefulWidget {

  const Form({
    Key key,
    @required this.child,
    this.autovalidate = false,
    this.onWillPop,
    this.onChanged,
  }) : assert(child != null),
       super(key: key);
    ...   
}
```

参数名字	| 参数类型	| 意义	| 必选 or 可选
- | - | - | -
key	| Key	| Widget 的标识	| 可选
child	| Widget	| Form 的子 Widget	| 必选
autovalidate |	bool	| 是否自动验证，默认为 false。true：每次输入有变动都会验证<br> false：只有调用 FormFieldState.validate 才会验证	 | 可选
onWillPop	| WillPopCallback	| 决定 Form 所在的路由是否可以直接返回（如点击返回按钮），<br>这个回调会返回一个 Future 对象，如果 Future 的最终结果是 false，<br>则当前路由不会返回；如果为 true，则会返回到上一个路由。此属性通常用于拦截返回按钮。 | 可选
onChanged	| VoidCallback	| Form 的任意一个 子FormField 内容发生变化时会触发此回调	| 必选
