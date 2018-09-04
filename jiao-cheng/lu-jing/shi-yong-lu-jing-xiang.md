# 使用路径项

在本教程中，我们将研究路径以及在 Paper.js 项目中创建和修改路径的不同方法。

### 剖析路径项

在 Paper.js 中，路径由一系列通过曲线连接的段表示。一个段由一个点和两个柄组成，定义了曲线的位置和方向。

[例子](http://paperjs.org/tutorials/paths/working-with-path-items/)

### 添加和插入段

为了开始路径学习，我们将使用没有定义柄的段，从而路径会通过直线而不是曲线连接。

我们使用`new Path()`构造函数来创建一个新的路径项，并使用`path.add(segment)`函数向其添加段：

```js
var myPath = new Path();
myPath.strokeColor = 'black';
myPath.add(new Point(0, 0));
myPath.add(new Point(100, 50));
```

![](/assets/path1.png)

add函数还支持多个参数，你可以一次插入多个段：

```js
var myPath = new Path();
myPath.strokeColor = 'black';
myPath.add(new Point(0, 0), new Point(100, 50));
```

要插入已有的段，可以使用`path.insert(index，segment)`函数：

```js
var myPath = new Path();
myPath.strokeColor = 'black';
myPath.add(new Point(0, 0), new Point(100, 50));

// 在路径中两个已存在的段之间插入一个新段
myPath.insert(1, new Point(30, 40));
```

> **请注意：**
>
> Point 对象表示 Paper.js 项目的二维空间中的一个点。 它不是路径中的锚点。 当 Point 传递给 add 或 insert 之类的函数时，它会动态转换为 Segment。 要了解有关 Point 对象的更多信息，请阅读 [点，尺寸和矩形](http://paperjs.org/tutorials/geometry/point-size-and-rectangle/)教程。



