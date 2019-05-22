### 加载 Flutter APP 中的图片

使用 Image.asset 加载本地图片。

1. 在 pubspec.yaml 中声明，图片的路径。
2. 在 .dart 文件中使用 Image.asset 引入本地图片即可。

``` yaml
# 如果图片很多的话，直接设置成目录即可（更推荐这种） - images/
assets:
  - images/a_dot_burr.jpeg
  - images/a_dot_ham.jpeg
```

``` dart
child: Image.asset(
  'images/avatar.jpg'
)
```
