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

### 点

Point 对象描述了二维坐标位置。 它有两个属性 x 和 y ，表示 x 和 y 的坐标位置。

可以通过直接提供 x 和 y 的坐标来创建点对象，也可以直接省略，这样 x 和 y 坐标会被初始化为0。坐标属性也可以单独访问和修改。

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



