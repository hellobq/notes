# Container 容器组件

[Container](https://docs.flutter.io/flutter/widgets/Container-class.html) 相当于浏览器中的 `div`。

### Alignment

规定容器子内容的对齐方式，并不是容器本身的对齐方式。

- bottomCenter:下部居中对齐。
- botomLeft: 下部左对齐。
- bottomRight：下部右对齐。
- center：纵横双向居中对齐。
- centerLeft：纵向居中横向居左对齐。
- centerRight：纵向居中横向居右对齐。
- topLeft：顶部左侧对齐。
- topCenter：顶部居中对齐。
- topRight： 顶部居左对齐。

``` dart
home: Scaffold(
  body: Center(
    child: Container(
      child: Text(
        'Hello Flutter',
        style: TextStyle(
          fontSize: 20.0
        )
      ),
      alignment: Alignment.bottomRight
    )
  )
)
```

### padding/margin

设置宽、高(浮点型数字)、背景颜色(支持ARGB颜色值/十六进制)、padding/margin:

``` dart
home: Scaffold(
  body: Center(
    child: Container(
      child: Text(
        'Hello Flutter',
        style: TextStyle(
          fontSize: 20.0
        )
      ),
      margin: const EdgeInsets.all(10.0),
      width: 200.0,
      height: 200.0,
      color: Colors.blue,
      padding: const EdgeInsets.all(20.0),
      alignment: Alignment.bottomRight
    )
  )
)
```

也可以使用 `EdgeInsets.fromLTRB(left, top, right, bottom)` 设置四个方向不同的值。

### decoration

设置背景和边框、边角：
- 用来设置背景时，就不需要使用 color 属性。
- 同时支持渐变色。

``` dart
decoration: BoxDecoration(
  color: Colors.blue,
  gradient: LinearGradient(
    colors: [Colors.blueAccent, Colors.amber, Colors.purpleAccent],
    begin: Alignment.centerLeft,
    end: Alignment.centerRight,
    tileMode: TileMode.mirror,
    stops: [0.1, 0.5, 0.8]
  )
)
```

设置边框：

``` dart
decoration: BoxDecoration(
  border: Border(
    left: BorderSide(color: Colors.blue),
    top: BorderSide(color: Colors.pink),
    right: BorderSide(color: Colors.red),
    bottom: BorderSide(color: Colors.green)
  )
)
```

也可以使用 Border.all(color: Colors.blue) 同时设置四边。
