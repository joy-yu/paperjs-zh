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

### 向量计算

如上简单例子所示，向量在数学计算中起到很大作用，可以将它们视为简单的值。 以下是一些不同可能的操作。

### 向量加法和向量减法

可以将一个向量和另一个向量相加，结果相当于将如何从一个地方到另一个地方的两个描述叠加在一起，从而产生第三个向量。

我们从四个点开始：

```js
var point1 = new Point(50, 0);
var point2 = new Point(40, 100);

var point3 = new Point(5, 135);
var point4 = new Point(75, 170);
```

与[点和向量](http://paperjs.org/tutorials/geometry/vector-geometry/#points-and-vectors)中的例子一样，我们现在可以通过点的相减来计算出两个向量：

```js
var vector1 = point2 - point1;
// = { x: 40, y: 100 } - { x: 50, y: 0 }
// = { x: -10, y: 100 }

var vector2 = point4 - point3;
// = { x: 75, y: 170 } - { x: 5, y: 135 }
// = { x: 70, y: 35 }
```

![](/assets/import5.png)

---

从 startPoint 开始，沿着 vector1 再沿着 vector2，我们可以先将 vector1 和 startPoint 相加，生成临时点 tempPoint，然后将vector2 和临时点 tempPoint 相加从而获得最终的 endPoint 点。

```js
var tempPoint = startPoint + vector1;
var endPoint = tempPoint + vector2;
```

但是如果我们想将同样的矢量组合应用于多个点，那么这样的计算会变得复杂，因为我们每次都必须经过临时变量 tempPoint，其实没有这个必要。

![](/assets/import6.png)

---

相反，我们可以将 vector1 和 vector2 相加，将结果对象用作描述组合运动的新向量。

```js
var vector = vector1 + vector2;
```

![](/assets/import7.png)

---

但是我们也可以做相反的事情，将两个矢量相减而不是相加。 结果相当于沿减去向量的相反方向一样。

```js
var vector = vector1 - vector2;
```

![](/assets/import8.png)

> **请注意：**
>
> 这些操作的结果相当于每个向量间的的 x、y 坐标值的相加减。 而不是长度、角度值的相加减。

### 向量乘法和向量除法

很容易想象数值乘法或除法应用于矢量会有什么作用：不是说“向那个方向走10米”，而是对应于“向该方向走10米的3倍”。 矢量乘法不会改变其角度。 它的长度是由乘值决定。

```js
var bigVector = smallVector * 3;
```

或者，另一种形式：

```js
var smallVector = bigVector / 3;
```

> **请注意：**
>
> 由于 Javascript 的限制，我们需要确保要乘法或除法的向量位于操作的左侧。 因为框架内部定义了运算返回的类型为运算符左侧的类型。 因此，下面的写法会产生无效结果：
>
> ```js
> var bigVector = 3 * smallVector;
> ```

![](/assets/import9.png)

### 修改向量长度

以上，我们了解到，向量的乘法或除法会改变向量的长度而不会修改角度。 但是我们也可以直接更改 vector 对象的 length 属性：

首先，我们通过直接使用 Point 构造函数创建一个向量，因为向量和点实际上是相同类型的对象：

```js
var vector = new Point(24, 60);
console.log(vector.length);
// 64.62198
```

现在我们改变向量的 length 属性。 这类似于前一个示例中的乘法，但这里直接修改了对象：

```js
vector.length = vector.length * 3;
console.log(vector.length);
// 193.86593
```

![](/assets/import10.png)

---

我们还可以将长度设置为固定值，将向量拉伸或缩小到此长度：

```js
vector.length = 100;
```

![](/assets/import11.png)

另一种改变向量长度的方法是使用[ point.normalize\(\)](http://paperjs.org/reference/point#normalize) 方法。 在数学中标准化向量即修改它的长度，使其长度为1。normalize\(\) 还接受一个可选参数，由此可以自定义长度。

我们从这一小节第一个示例第一行的相同向量开始。我们来看看这个向量标准化版本：

```js
var vector = new Point(24, 60); 
var normalizedVector = vector.normalize();
console.log(vector.length);
// 64.62198
console.log(normalizedVector.length);
// 1
```

请注意，normalizedVector 的长度现在为1，而原始向量保持不变。normalize\(\)不会修改它所调用的向量，而是返回一个新的标准化向量对象。

现在，如果我们将标准值设为10，会发生什么？

```js
var normalizedVector = vector.normalize(10);
console.log(normalizedVector.length);
// 10
```

正如预期的那样，返回的向量的长度为10。注意，我们也可以将第一个标准化向量 normalizedVector 乘以10：

```js
var normalizedVector = vector.normalize() * 10;
console.log(normalizedVector.length);
// 10
```

### 旋转向量和使用角度

旋转向量是用于构造路径和形状的强大工具，我们可以基于某个方向来旋转一定的角度，从而定义一个新的相对方向，例如侧向。[ 使用鼠标向量](http://paperjs.org/tutorials/interaction/working-with-mouse-vectors/)教程里有一个很好的示例，示例中旋转矢量用来构造与鼠标移动方向和位置平行的路径。

Paper.js 中的所有角度都以度为单位，并且以顺时针方向旋转。 角度值从水平轴开始并向下扩展。 在 180° 时，角度值会翻转到 -180°，它们俩是一样的，沿左方向或右方向绕一圈可以旋转到相同的位置。 不过这也不影响你将角度设置为180°的更高值。

![](/assets/import12.png)

有两种方法可以改变向量的角度。 最直观的是将向量的 angle 属性设置为一个新值。 我们首先设置一个向下 100，向右 100 的向量，并记录其角度和长度：

```js
var vector = new Point(100, 100);
console.log(vector.angle);
// 45
```

由于我们向下值和向右值等量，它的角度为45°。 让我们记录它的长度，以便我们旋转向量后再来观察：

```js
console.log(vector.length);
// 141.42136
```

![](/assets/import13.png)

---

现在我们将其角度顺时针旋转 90°，设置为 45°+ 90°= 135° ，再次记录长度：

```js
vector.angle = 135;
console.log(vector.length);
// 141.42136
```

注意到长度没有改变。 我们改变的只是向量的方向。 如果我们再次打印整个矢量，我们会发现它的坐标不再相同：

```js
console.log(vector);
// { x: -100, y: 100 }
```

![](/assets/import14.png)

---

我们可以明确地给它增加90°，而不是直接将角度设置为 135：

```js
vector.angle = vector.angle + 90;
```

一种更简单的方法是使用 += 运算符，这样可以避免写两次 vector.angle：

```js
vector.angle += 90;
```

![](/assets/import15.png)

### 运算符，方法和属性

注意，数学运算（加法，减法，乘法和除法）与诸如`rotate()`和`normalize()`之类的方法不会修改涉及的向量和点对象。 相反，它们将结果作为新对象返回。这意味着它们可以在表达式中链接和组合：

```js
var point = event.middlePoint
		+ event.delta.rotate(90);
```

另一方面，修改向量的角度或长度会直接修改向量对象，并且只能在此类表达式之外使用。 由于我们直接修改了对象，因此我们需要注意修改的内容，如果不希望修改原始对象，可以使用`clone()`函数。

```js
var delta = event.delta.clone();
delta.angle += 90;
var point = event.middlePoint + delta;
```

### Vektor.js

下面的脚本示例可以帮助您熟悉向量的概念。

尽情使用它从而了解向量如何工作，并尝试使用它来重现本教程中学到的原理。

🌰例子在[这里](http://paperjs.org/tutorials/geometry/vector-geometry/)

