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

### 平滑路径

Paper.js 中你可以使用`path.smooth()`函数自动平滑路径。 这个函数可以计算出路径分段点的柄的最佳值，从而生成平滑经过的曲线。 段不会移动，路径段当前的柄设置会被忽略。

在下面的示例中，我们创建一个矩形路径，创建它的副本对象并平滑副本对象：

```js
var path = new Path();
path.strokeColor = 'black';
path.add(new Point(30, 75)); 
path.add(new Point(30, 25)); 
path.add(new Point(80, 25));
path.add(new Point(80, 75));
path.closed = true;

// 选中路径，从而观察它的柄
path.fullySelected = true;

// 创建一份路径的拷贝，并向右移动100像素
var copy = path.clone();
copy.fullySelected = true;
copy.position.x += 100;

// 平滑路径的段
copy.smooth();
```

![](/assets/path2.png)

### 闭合路径

默认情况下，通过`new Path()`构造函数创建的路径是打开的：

```js
var myPath = new Path();
myPath.strokeColor = 'black';
myPath.add(new Point(40, 90));
myPath.add(new Point(90, 40));
myPath.add(new Point(140, 90));
```

![](/assets/path3.png)

要闭合路径，我们将其 path.closed 属性设置为 true。 随后 Paper.js 将连接路径的第一段和最后一段：

```js
var myPath = new Path();
myPath.strokeColor = 'black';
myPath.add(new Point(40, 90));
myPath.add(new Point(90, 40));
myPath.add(new Point(140, 90));

myPath.closed = true;
```

![](/assets/path4.png)

### 移除段和路径

要从路径中删除段，我们使用`path.removeSegment(index)`函数，我们把要删除的段的索引传递给它。

> **请注意：**
>
> 如果您还不知道如何创建预定义形状的路径，请阅读[创建预定义形状](http://paperjs.org/tutorials/paths/creating-predefined-shapes/)教程。

首先，我们创建一个圆形路径并并观察它的段：

```js
var myCircle = new Path.Circle(new Point(100, 70), 50);
myCircle.strokeColor = 'black';
myCircle.selected = true;
```

![](/assets/path5.png)

如你所见，路径有4个段。

现在，让我们在创建后删除路径的第一段：

```js
var myCircle = new Path.Circle(new Point(100, 70), 50);
myCircle.strokeColor = 'black';
myCircle.selected = true;

myCircle.removeSegment(0);
```

![](/assets/path6.png)

> **你知道吗？**
>
> 在 Javascript 和其他大多数编程语言中，当我们引用列表项的索引时，我们总是从0开始计数。 0是第一项，1是第二项，等等。

如果想把它从项目中完全删除项目，我们使用`item.remove()`：

```js
var myCircle = new Path.Circle(new Point(100, 100), 50);
myCircle.fillColor = 'black';

myCircle.remove();
```



