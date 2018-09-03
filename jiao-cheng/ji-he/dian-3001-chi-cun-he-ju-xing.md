# 点、尺寸和矩形

在 Paper.js 中，[Point](http://paperjs.org/reference/point)，[Size](http://paperjs.org/reference/size) 和 [Rectangle](http://paperjs.org/reference/rectangle) 等基本类型是描述图形项几何属性的对象。它们是几何值的抽象表示，例如位置和尺寸，但不直接表示项目中的图形项。

> **请注意：**
>
> Paper.js 项目中的图形项是显示在图层列表中并在项目中可见的项。可以和现实世界中的“物理”项进行类比。为了描述它们的位置和尺寸，Paper.js 配置了不同的基本类型，这些类型只是描述其几何特性的数值容器。

这意味着当我们在代码中创建一个 [Point](http://paperjs.org/reference/point) 对象时，我们实际上只是在视图中创建一个位置的描述，但我们没有创建一个包含该点作为段的路径项：

```js
var myPoint = new Point(10, 20); 
console.log(myPoint); // { x: 10, y: 20 }
```

为了创建包含该点作为段的路径项，我们需要显式使用 [new Path\(\)](http://paperjs.org/reference/path#path) 构造函数来创建路径并将该点作为第一个段添加到其中。[“使用路径项”](http://paperjs.org/tutorials/paths/working-with-path-items/)教程更详细地描述了路径和段有关的内容。

```js
var myPath = new Path();
myPath.add(myPoint);
```

执行此脚本，将在 Paper.js 项目中生成一个“物理”路径项，myPoint 的位置会生成一个段。

> **请注意：**
>
> 同样的，myPath 中“物理”上出现的段和名为 myPoint 的点不一样。myPoint 只是用于描述生成 myPath 第一段的坐标。如果段已经产生，修改 myPoint 不会改变这个段。

### 点（Point）

Point 对象描述了二维空间的坐标位置。 它有两个属性 x 和 y ，表示 x 和 y 的坐标位置。

可以通过直接提供 x 和 y 的坐标来创建 Point 对象，也可以直接省略，这样 x 和 y 坐标会被初始化为0。坐标属性也可以单独访问和修改。

这里我们创建了一个新点，不提供 x 和 y 的值，之后修改它们的值。`console.log()`函数用于将结果值记录到控制台。

```js
var myPoint = new Point();
console.log(myPoint); // { x: 0, y: 0 }

// 现在我们改变 x 坐标值为 10...
myPoint.x = 10;

// ...y 坐标值为 x + 10
myPoint.y = myPoint.x + 10;
console.log(myPoint); // { x: 10, y: 20 }
```

> **你知道吗？**
>
> `console.log()`函数将文本发送到浏览器的控制台，这对调试脚本非常有用。

这里，我们创建一个新点并定义坐标位置，然后进行修改。

```js
var myPoint = new Point(20, 40);
console.log(myPoint); // { x: 20, y: 40 }

// 现在我们将 x 坐标位置扩大两倍
myPoint.x = myPoint.x * 2;
console.log(myPoint); // { x: 40, y: 40 }
```

创建 point 对象的另一种方法是将现有点传递给构造函数，新点将成为副本。 更改新点不会修改原来的点：

```js
var firstPoint = new Point(20, 40);
var secondPoint = new Point(firstPoint);
console.log(secondPoint); // { x: 20, y: 40 }

secondPoint.y = 20;
console.log(secondPoint); // { x: 20, y: 20 }

// Note that firstPoint has not changed:
console.log(firstPoint); // { x: 20, y: 40 }
```

这与简单的变量引用不同，后者不会进行复制：

```js
var firstPoint = new Point(20, 40);
var secondPoint = firstPoint;
secondPoint.y = 20;
console.log(secondPoint); // { x: 20, y: 20 }

// 第一个点的位置也改变了:
console.log(firstPoint); // { x: 20, y: 20 }
```

> **请注意：**
>
> Paper.js 中的所有基本类型都有这样的复制构造函数。一种更简单方法是在任何对象上调用`clone()`函数，这样可以产生对象副本，避免直接修改变量引用：

```js
var firstPoint = new Point(20, 40);
var secondPoint = firstPoint.clone();
```

### 尺寸（Size）

Size 对象描述的事二维空间中的抽象维度。它有两个属性 width 和 height ，表示尺寸的宽、高值。

就像使用 Point 对象一样，可以通过直接提供 width 和 height 值来创建 Size 对象，也可以直接省略，这样 width 和 height 值会被初始化为0。宽度和高度属性也可以单独访问和修改。 例如，上一小节关于 Point 对象的相同步骤在这里可以使用 Size 对象替换执行。 关于 Point 对象的说明同样适用于 Size 对象，唯一的区别是属性名称的不同。

```js
var mySize = new Size();
console.log(mySize); // { width: 0, height: 0 }

mySize.width = 10;
mySize.height = mySize.width + 10;
console.log(mySize); // { width: 10, height: 20 }
```

```js
var mySize = new Size();
console.log(mySize); // { width: 0, height: 0 }

mySize.width = 10;
mySize.height = mySize.width + 10;
console.log(mySize); // { width: 10, height: 20 }
```

### 矩形（Rectangle）

Rectangle 对象可以描述为 Point对象和 Size 对象的组合，描述二维空间的位置和尺寸。 因此它具有x，y，width，height 四个属性。 属性 x 和 y 描述矩形左上角的坐标，width 和 height 描述其尺寸。 此外，它还定义了 point 和 size 属性，可以以 Point和 Size 对象的形式访问这些值。 

创建 Rectangle 对象有多种方式。 一种是将 Point 和 Size 对象传递给`new Rectangle(point,size)`构造函数：

```js
var topLeft = new Point(10, 20);
var rectSize = new Size(200, 100);
var rect = new Rectangle(topLeft, rectSize);
console.log(rect); // { x: 10, y: 20, width: 200, height: 100 }
console.log(rect.point); // { x: 10, y: 20 }
console.log(rect.size); // { width: 200, height: 100 }
```

可以使用`new Rectangle(x,y,width,height)`构造函数创建相同的 Rectangle 对象：

```js
var rect = new Rectangle(10, 20, 200, 100);
console.log(rect); // { x: 10, y: 20, width: 200, height: 100 }
```

第三种是使用`new Rectangle(point1,point2)`构造函数，它接收 Rectangle 对象的两个对角点。 不一定非得是左上角和右下角，构造函数可以通过这两点的计算生成矩形：

```js
var bottomLeft = new Point(10, 120);
var topRight = new Point(210, 20);
var rect = new Rectangle(bottomLeft, topRight);
console.log(rect); // { x: 10, y: 20, width: 200, height: 100 }
```

> **请注意：**
>
> new 出来的基本类型不一定需要每次都放入命名的变量中。 我们可以直接将它们传递给 Rectangle 构造函数。
>
> ```js
> var rect = new Rectangle(new Point(10, 120), new Point(210, 20));
> ```

### 矩形属性

Rectangle 对象比 Point 和 Size 对象稍微复杂一些，同时提供了一系列额外的中心和对角点对象：center，topLeft，topRight，bottomLeft，bottomRight，leftCenter，topCenter，rightCenter 和 bottomCenter。

创建矩形后，可以更改所有这些值，可以简便地指定矩形几何特性：

```js
// 创建一个矩形
// 大小尺寸都初始化为0
var rect = new Rectangle();
console.log(rect); // { x: 0, y: 0, width: 0, height: 0 }

// 现在我们可以定义它的大小...
rect.size = new Size(100, 200);

// 和它的中心点
rect.center = new Point(100, 100);
console.log(rect); // { x: 50, y: 0, width: 100, height: 200 }
```

作为定义矩形尺寸的替代数字方式，Rectangle 对象还提供了与x，y，width 和 height 相对的属性：left，top，right 和 bottom：

```js
var rect = new Rectangle();
rect.left = 100;
rect.right = 200;
rect.bottom = 400;
rect.top = 200;
console.log(rect); // { x: 100, y: 200, width: 100, height: 200 }
```



