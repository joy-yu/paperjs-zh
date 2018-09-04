# 创建预定义的形状

Paper.js 中你可以使用各种预定义的形状创建路径项。

与`new Path()`构造函数创建没有点的空路径的方式相同，我们有诸如`new Path.Circle(center, radius)`和`new Path.Rectangle(point, size)`的构造函数，它们创建路径并且自动给路径添加段，从而创建预定义的形状。

### 圆形路径

使用`new Path.Circle(center, radius)`构造函数，我们可以生成圆形路径。

下面的代码生成了一个圆形路径，其中心点位于 {x: 100, y: 70}，半径为 50 pt：

```js
var myCircle = new Path.Circle(new Point(100, 70), 50);
myCircle.fillColor = 'black';
```

### 矩形路径

要创建矩形路径，可以将 Rectangle 传递给`new Path.Rectangle(rect)`构造函数。

> **请注意：**
>
> Rectangle 对象是矩形的抽象表示。 请阅读[点，尺寸和矩形](http://paperjs.org/tutorials/geometry/point-size-and-rectangle/)教程以了解如何使用 Rectangle 对象。

例如，我们在 {x: 0, y: 0} 和 {x: 50, y: 50} 之间创建一个矩形，然后使用`new Path.Rectangle(rect)`构造函数创建一个描述它形状的路径：

```js
var rectangle = new Rectangle(new Point(50, 50), new Point(150, 100));
var path = new Path.Rectangle(rectangle);
path.fillColor = '#e9e9ff';
path.selected = true;
```

![](/assets/shape1.png)

### 圆角矩形路径

要创建带圆角的矩形路径，我们使用`new Path.RoundedRectangle(rect, size)`构造函数。 rect 参数描述 Rectangle，size 参数描述圆角的尺寸。

例如，下面的脚本创建了一个具有20 pt \* 20 pt 角的圆角矩形路径：

```js
var rectangle = new Rectangle(new Point(50, 50), new Point(150, 100));
var cornerSize = new Size(20, 20);
var path = new Path.RoundRectangle(rectangle, cornerSize);
path.fillColor = 'black';
```

### 正多边形路径

要创建规则的多边形路径，我们使用`new Path.RegularPolygon(center, numSides, radius)`构造函数。

center 参数描述多边形的中心点，numSides 参数描述多边形的边数量，radius 参数描述多边形的半径。

例如，让我们创建一个三角形路径和一个十边形路径：

```js
// 创建三角形路径
var triangle = new Path.RegularPolygon(new Point(80, 70), 3, 50);
triangle.fillColor = '#e9e9ff';
triangle.selected = true;

// 创建十边形路径
var decagon = new Path.RegularPolygon(new Point(200, 70), 10, 50);
decagon.fillColor = '#e9e9ff';
decagon.selected = true;
```

> **你知道吗？**
>
> 你可以查看[路径引用](http://paperjs.org/reference/path)的构造函数部分，以获取 Path 构造函数的完整列表。



