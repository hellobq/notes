# 各大数据类型的 API

和 js 相似，即使是一个字面量也可以使用对象的 API，因为它会先转变成临时对象，这个临时对象的 API就是该数据类型的 API。

## 数字类型 API

num 分为：int、double。(也可用 num 声明变量)

当且仅当this是奇数时，返回true。

    bool isOdd

num 转 字符串：

    String toString();

数字字符串 other 转数字(不是数字字符串将报错)：
    num/int/double.parse(String other);

int 转换成 radix 进制的数字，同时转为字符串：   

    String toRadixString(int radix);

返回 num 的绝对值:
    num abs();

四舍五入，返回最接近this的整数:

    int round();

向下取整，返回不大于this的最大整数：

    int floor();  // truncate()/toInt() 与之类似

向上取整，返回不小于this的最小整数：

    int ceil();

是否是有限值:     
    
    int isFinite(); // 无限值：NaN/INFINITY/-INFINITY

是否是 NaN:

    int isNaN();

将 num 作为 double 值返回。

    double toDouble();

保留 fractionDigits 位小数，即四舍五入 fractionDigits 位，并以字符串形式返回:

    String toStringAsFixed(int fractionDigits)

相关链接：[dart double](http://www.shutongye.com/dartapi/dart-core/double/truncate.html)

## 字符串类型

判断字符串是否为空：

    bool isEmpty

获取字符串长度：

    int length

判断字符串是否包含 other:

    bool contains(Pattern other, [int startIndex = 0]);

判断字符串是否以 other 为结尾：

    bool endsWith(String other);

如果字符串以 pattern 的匹配开始，返回true:

    bool startsWith(Pattern pattern, [int index = 0]);

从前匹配：返回字符串中，从start（包括，不能是负数或大于 length）开始，pattern第一次匹配到的位置（未匹配到，则返回 -1）：

    int indexOf(Pattern pattern, [int start=0]);

从后匹配：返回字符串中，从start（包括）至0，pattern第一次匹配到的位置：

    int lastIndexOf(Pattern pattern, [int start=length]);

将字符串中所有的字符转换为大/小写:

    String toLowerCase();
    String toUpperCase();

按照正则 pattern 切割，返回字符串列表：

    List<String> split(Pattern pattern);

[startIndex, endIndex) 截取 this (字符串)：

    String substring(int startIndex, [int endIndex=length])

去除左右空格：

    String trim();
    String trimLeft();
    String trimRight();

相关链接：[dart String](http://www.shutongye.com/dartapi/dart-core/String/substring.html)

## List 列表类型（也是容器）

获取列表长度：

    int length

列表反转成 Iterable 对象:

    Iterable <E> reversed

在List的末尾添加value，并扩展1个长度:

    void add(E value);

将 iterable 的所有对象附加到List的末尾，通过 iterable 中对象的数量来扩展 List 的长度:

    void addAll(Iterable<E> iterable);

删除 List 中的所有对象，并且 List 长度变成0。如果 this 是一个固定长度的 List，会抛出 UnsupportedError ，并保留所有对象：

    void clear();

在List中的index位置插入对象。这会增加一个List的长度，并将索引处及索引之后的所有对象，向List末尾移动。如果index小于0或大于长度，将出错:

    void insert(int index, E element);

在List中的index位置插入iterable的所有对象。这会增加List的长度（length加上iterable的长度）， 并将所有之后的对象向List末尾移动。如果index小于0或大于长度，将出错:

    void insertAll(int index, Iterable<E> iterable);

删除List中第一次出现的value:

    bool remove(Object value);

删除最后一个元素，返回删除的元素:

    E removeLast();

删除List中 index ([0, length])索引处的对象。返回被删除的对象:

    E removeAt(int index);

删除 [start, end) 范围内的对象:

    void removeRange(int start, int end);

删除 [start, end) 范围内的对象， 并在它的位置插入 replacement 的内容:

    void replaceRange(int start, int end, Iterable<E> replacement);

设置 [start, end) 范围的对象为fillValue。如果 start..end 并不是 this 一个有效的范围，将出错:

    void fillRange(int start, int end, [E fillValue]);

排序：

    void sort([int compare(E a, E b)]);

将每个元素转换成 separator 并连接:

    String join([String separator = ""])

相关链接：[dart List][](http://www.shutongye.com/dartapi/dart-core/List/shuffle.html)

## Map 数据类型（也是容器）

获取 map 长度：

    int length

判断是否为空：

    bool isEmpty
    bool isNotEmpty

反馈 iterable 对象的 keys/values:

    iterable keys
    iterable values

将 other 中所有的 key-value 键值对添加到 this 中。如果 other 的某个 key 已经存在于 this，它的值会被重写。

    void addAll(Map<K, V> other);

如果存在的话，从 Map 中删除 key 和它关联的 value 。返回 key 被删除前关联的 value 。如果 key 不存在于 Map 中，返回 null。请注意，如果值可以为 null，那么返回 null 并不总是意味着 key 不存在。

    V remove(Object key);

如果 thi s包含指定的 key，返回 true。如果 Map 中的任何一个 key 根据 == 运算操作，等于 key，则返回 true。

    bool containsKey(Object key);

如果 this 包含指定的 value，返回 true。如果 Map 中的任何一个 value 根据==运算操作，等于 value，则返回 true。

    bool containsValue(Object value);

删除 Ma p中所有的键值对。在执行此操作之后，Map 为空。

    void clear();

相关链接：[dart Map][](http://www.shutongye.com/dartapi/dart-collection/MapMixin/clear.html)

## Set 容器

集合：无序、唯一。

将 value 添加到 Set 中。如果 value（或相等的值）还不在Set中，返回true。 否则，返回false，并且Set不变。

    bool add(E element);

将所有 elements 添加到 Set 中。

    void addAll(Iterable<E> elements);

从Set中删除value。 如果value在Set中，返回true。否则，返回false。 如果value不在Set中，方法不会产生任何效果。

    bool remove(Object element);

如果value在Set中，返回true。

    bool contains(Object element);

返回this是否包含other的所有元素。

    bool containsAll(Iterable<Object> other);

返回this和other的差集。

    Set<E> difference(Set<Object> other);

通过索引返回元素。index不能为负值，并且小于length。

    E elementAt(int index);

如果元素中任何一个使test返回false，该方法返回false。 否则返回true。

    bool every(bool f(E element));

对集合的每个元素，按迭代顺序应用f函数。

    void forEach(void f(E element));

将每个元素转换成String并连接。

    String join([String separator = ""]);

转List。

    List<E> toList({bool growable: true})
