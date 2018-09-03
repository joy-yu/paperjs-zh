# 向量几何

向量几何是 Paper.js 中的一等公民。 在学习编写脚本的同时，了解其基本原理有很大的好处。 毕竟，在“矢量图形”这个词中包含着“矢量”这个词。

在构建 [Scriptographer](http://scriptographer.org/) 时，我们发现向量几何是一种处理位置、运动和路径的强大方法。一旦理解它，你会发现它比直接使用坐标系的x值和y值更加直观和灵活，就像那些视觉导向的编程环境那样。

这里是一个刷子工具的交互式示例，他是向量几何的一个优雅示例。 只有24行代码，它生成一种鼠标工具，使用起来会像刷子一样，他有可变化的厚度，这取决于速度和某种天然展现。

在下面的视图中单击并拖动：

🌰🌰🌰🌰🌰🌰🌰🌰🌰🌰🌰🌰🌰🌰🌰🌰🌰🌰🌰🌰🌰🌰🌰🌰🌰栗子暂没有迁移，[点击查看原网页](http://paperjs.org/tutorials/geometry/vector-geometry/)

此脚本是在[使用鼠标向量](http://paperjs.org/tutorials/interaction/working-with-mouse-vectors/)教程中一步步开发的，包含每行代码的相关说明。 在查看这样一个应用示例之前，了解下面概述的向量几何基本原理至关重要。

### 点和向量

在许多方面，向量与点非常相似。 两者都由 x 和 y 坐标表示。 但是点描述绝对位置，但矢量表达一种相对信息：是从一个点到另一个点的表达。 下面是解释向量与点之间关系的分步示例。

我们首先创建两个Point对象来描述文档中的两个绝对位置，由它们的 x y 坐标值定义：

```js
var point1 = new Point(50, 50);
var point2 = new Point(110, 200);
```

![](/assets/import.png)

---

为了从 point1 到 point2，我们可以说我们需要向右移动60（在x方向上），向下移动150（在y方向上）。 这些值是从点 point2 减去点 point1 的 x 坐标值和 y 坐标值的结果：

```js
var x = point2.x - point1.x;
// = 110 - 50 = 60
var y = point2.y - point1.y;
// = 200 - 50 = 150;
```

换句话说，通过将这两个值添加到 point1 坐标，最终得到了 point2。

![](/assets/import2.png)

---

和使用这两个单独的值相比，使用向量作为它们的容器要容易得多。 要计算此向量，我们可以简单地从 point2 中减去 point1，而不是在上一步中减去两个单独的减法：

```js
var vector = point2 - point1;
// = { x: 110, y: 200 } - { x: 50, y: 50 }
// = { x: 60, y: 150 }
```

![](/assets/import3.png)

> **请注意：**
>
> 你可以阅读[数学运算](http://paperjs.org/tutorials/geometry/mathematical-operations/#mathematical-operations)教程以了解有关数学运算的更多内容。
>
> 这个减法（矢量）的结果仍然是Point对象。 从技术上讲，点和矢量之间没有区别。 变化只是它们的含义：一个点是绝对的，一个矢量是相对的。

---

矢量也可以描述为箭头。 与箭头类似，它们指向某个方向，并且还指示在该方向上移动的距离量。 因此，我们通常使用一种更有效的方式来描述矢量：角度和长度。

Point 对象提供了 point.angle 和 point.length 这两种属性表示，并且它们都可以修改。

```js
console.log(vector.length);
// 161.55494
console.log(vector.angle);
// 68.19859
```

> **请注意：**
>
> 默认情况下，Paper.js 中的所有角度都以度为单位。 你可以阅读[旋转向量](http://paperjs.org/tutorials/geometry/vector-geometry/#rotating-vectors-and-working-with-angles)章节，了解更多有关角度和旋转的信息。

重要的点我们再重复一遍：向量包含的是相对信息。 向量告知我们方向以及移动距离。

使用向量最简单的方式就是：把它与一个绝对位置的点相加。 结果是又一个绝对位置的点，这个点位于从起始点偏移指定向量信息的位置。 以这种方式，我们可以将相同的向量和许多点相加，如下图所示。 你看到的向量都是相同的，但将它与一组不同位置的点相加所得到的点位置也都不同。

![](/assets/import4.png)

