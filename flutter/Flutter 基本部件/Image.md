### ImageProvider

`ImageProvider` 是一个抽象类，主要定义图片数据获取的接口 `load()`，从不同的数据源获取图片的接口不同。

- `AssetImage` 从 `asset` 中加载图片。
- `NetworkImage` 从网络中加载图片。

### Image

Image 用来加载图片的部件，加载图片的方式有多种：网络、文件、内存、asset。Image 类总共有 5 个构造函数：

``` dart
class Image extends StatefulWidget {

  const Image({
    @required this.image,
    ...
  })
  
  // 从网络中加载 image
  Image.network(String src,{
    ...
  })
  
  // 从本地文件中加载图片，此时需要提供本地图片地址
  Image.file(File file, {
    ...
  })
  
  // 从 Flutter APP 中加载图片资源
  Image.asset(String name, {
    ...
  })
  
  // 从内存加载图片，需要入图片的 bytes 数据，类型是 Uint8List
  Image.memory(Uint8List bytes, {
    ...
  })
}
```

一般只是用四种命名构造函数，四种不同的构造函数表明图片的来源不同。

### 构造函数的共有参数

参数名字	| 参数类型	| 意义	| 必选 or 可选
- | - | - | -
key	| Key |	Widget 的标识	| 可选
width	| double	| 图片的宽<br>如果为null的话，则图像将选择最佳大小显示，而且会保留其固有宽高比的大小 | 可选
height	| double	| 图片的高<br>如果为null的话，则图像将选择最佳大小显示，而且会保留其固有宽高比的大小	| 可选
color	| Color	| 图片的混合色值	| 可选
colorBlendMode | BlendMode	| 图片与颜色的混合模式	| 可选
fit	| BoxFit	| 用于在图片的显示空间和图片本身大小不同时指定图片的适应模式	| 可选
alignment	| Alignment	| [图片的对齐方式](Container.md)	| 可选
repeat	| ImageRepeat	| 当图片本身大小小于显示空间时，指定图片的重复规则 | 可选
scale |	double	| 图形缩小的比例，值越大图越小	| 可选
semanticsLabel	| String	| 给 Image 加上一个语义标签，没有实际用处	| 可选
centerSlice |	Rect	| 在这个矩形范围内的图片会被当成.9的图片 |	可选
matchTextDirection	| bool	| 图片的绘制方向<br>true:从左往右<br>false:从右往左	| 可选
gaplessPlayback	| bool |当图像提供者更改时<br>true：继续显示旧图像<br>false：简单地显示任何内容 | 可选
filterQuality	| FilterQuality	| 设置图片的过滤质量	| 可选

#### fit：BoxFit，用于在图片的显示空间和图片本身大小不同时指定图片的适应模式

BoxFit 的值 | 含义
- | - | -
BoxFit.fill	| 会拉伸直至填充满显示空间，图片本身长宽比会发生变化，图片会变形。
BoxFit.contain	| 图片会等比缩放撑满父部件的一边（最优）
BoxFit.cover	| 让图片覆盖父部件可视区域，图片多余的部分将会被裁剪
BoxFit.fitWidth |	图片的宽度会缩放到显示空间的宽度，高度会按比例缩放，然后居中显示，图片不会变形，如果超出显示空间部分会被剪裁
BoxFit.fitHeight |	图片的高度会缩放到显示空间的高度，宽度会按比例缩放，然后居中显示，图片不会变形，如果超出显示空间部分会被剪裁。
BoxFit.scaleDown	| 对齐目标框内的源（默认情况下，居中），并在必要时缩小源以确保源适合框内。这与contains相同，如果这会缩小图像，否则它与none相同。
BoxFit.none	| 图片没有适应策略，会在显示空间内显示图片，如果图片比显示空间大，则显示空间只会显示图片中间部分

#### repeat：ImageRepeat，当图片本身大小小于显示空间时，指定图片的重复规则

ImageRepeat的值	| 含义
- | - | -
ImageRepeat.repeat	| 在x和y轴上重复图像，直到填充满空间。
ImageRepeat.repeatX	| 在x轴上重复图像，直到填充满空间。
ImageRepeat.repeatY	| 在y轴上重复图像，直到填充满空间。
ImageRepeat.noRepeat	| 不重复

#### filterQuality：FilterQuality，设置图片的过滤质量（没啥用）

FilterQuality的值	| 含义
- | - | -
FilterQuality.none	| 最快的过滤。
FilterQuality.low	| 比none的过滤质量好，但是比none的时间要长。
FilterQuality.medium	| 比low的过滤质量好，但是也比low的时间要长
FilterQuality.high	| 过滤质量最高，但也最慢
