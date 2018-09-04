# 使用颜色和样式

下面的教程中，我们将研究在项目中给项目添加样式的不同方法。

### 示例路径

本教程中的示例，我们将使用以下代码创建的复选标记形状路径：

```js
var myPath = new Path({
	segments: [[40, 115], [80, 180], [200, 20]],
	selected: true
});
```

![](/assets/style1.png)

> **请注意：**
>
> 要了解如何使用 Paper.js 创建路径，请阅读[使用路径项](http://paperjs.org/tutorials/paths/working-with-path-items/)教程。

### 笔划颜色

要在我们的路径中添加笔划，我们需要设置其 strokeColor 属性。

下面的示例演示如何使用十六进制字符串（可从 HTML CSS 样式中了解）将我们之前创建的路径的笔划颜色设置为红色。

```js
var myPath = new Path({
	segments: [[40, 115], [80, 180], [200, 20]]
});

myPath.strokeColor = '#ff0000'; // 红色
```

![](/assets/style2.png)

十六进制颜色代码会自动转换为 Color 对象。

也可以直接使用 Color 对象设置颜色。 在下面的代码中，我们设置了RGB颜色，红色为50％，绿色为0％，蓝色为50％：

```js
var myPath = new Path({
	segments: [[40, 115], [80, 180], [200, 20]]
});

myPath.strokeColor = new Color(0.5, 0, 0.5);
```

![](/assets/style3.png)

> **请注意：**
>
> Paper.js 中，颜色分量值的范围为0到1。

### 填充颜色

填充颜色的工作方式与笔划颜色完全相同。 下面的示例中，我们将创建一个填充红色的路径：

```js
var myPath = new Path({
	segments: [[40, 115], [80, 180], [200, 20]],
	selected: true
});

myPath.fillColor = '#ff0000';
```

![](/assets/style4.png)

### 笔划宽度

要更改路径的笔划宽度，可以更改其 strokeWidth 属性。

下面的例子中，我们给路径一个 10pt 的红色笔划：

```js
var myPath = new Path({
	segments: [[40, 115], [80, 180], [200, 20]]
});
myPath.strokeColor = '#ff0000';
myPath.strokeWidth = 10;
```

![](/assets/style5.png)

### 笔划头

要更改路径开头和结尾的形状，可以将 strokeCap 属性更改为 "round"，"square" 或 "butt"：

```js
var myPath = new Path({
	segments: [[40, 115], [80, 180], [200, 20]],
	selected: true
});

myPath.strokeColor = '#ff0000';
myPath.strokeWidth = 10;

myPath.strokeCap = 'round';
```

![](/assets/style6.png)

### 笔划连接

要更改路径中角的形状，可以将 strokeJoin 属性更改为 "miter"，"round" 或 "bevel"：

```js
var myPath = new Path({
	segments: [[40, 115], [80, 180], [200, 20]],
	selected: true
});

myPath.strokeColor = '#ff0000';
myPath.strokeWidth = 10;

myPath.strokeJoin = 'round';
```

![](/assets/style7.png)

### 虚线笔划

要创建虚线笔划，可以更改项目的 dashArray 属性。 以下代码生成一个带有 10pt 短划线和 12pt 间隙的虚线笔划：

```js
var myPath = new Path({
	segments: [[40, 115], [80, 180], [200, 20]],
	selected: true
});

myPath.strokeColor = '#ff0000';
myPath.strokeWidth = 5;
myPath.strokeCap = 'round';

myPath.dashArray = [10, 12];
```

### PathStyle 对象

每个项都有一个 item.style 属性，它是一个只包含样式属性的对象。

我们可以使用它来将一个项的样式属性复制给另一个项。 下面的示例首先创建一个圆形路径并为其指定一种笔划颜色。 然后创建另一个圆形路径，我们为它指定第一个路径的样式：

```js
var firstPath = new Path.Circle({
	center: [80, 50],
	radius: 35
});

firstPath.strokeColor = '#ff0000';
firstPath.fillColor = 'blue';

// secondPath 暂时没有笔划颜色
var secondPath = new Path.Circle({
	center: [160, 50],
	radius: 35
});

// 给 secondPath 应用 firstPath 的样式：
secondPath.style = firstPath.style;
```

![](/assets/style8.png)

item.style 属性也可以一次性设置多个样式属性。

下面的示例中，我们创建一个包含多个样式属性的对象，并将其赋值给 myCircle 的 style 属性，这样可以一次性设置多个样式：

```js
var myStyle = {
	strokeColor: '#00ffff',
	fillColor: '#000000',
	strokeWidth: 50
};

var myCircle = new Path.Circle({
	center: [100, 100],
	radius: 50
});
myCircle.style = myStyle;
```

![](/assets/style9.png)

### 移除样式

想要删除任意路径样式，只需将指定样式属性赋值为 null：

```js
var path = new Path.Circle({
	center: new Point(50, 50),
	radius: 50
});
path.fillColor = 'red';

// Set the fillColor to null to remove it:
path.fillColor = null;
```

想要删除路径的所有样式，可以将 style 属性赋值为 null：

```js
var path = new Path.Circle({
	center: [50, 50],
	radius: 50
});
path.style = null;
```

### 使用当前项目的风格

正如我之前提到的，所有新创建的项都会自动接受 Illustrator 接口中定义的当前活动路径样式属性。 我们也可以使用 currentStyle，通过代码来更改这些样式。

currentStyle 是项目的 PathStyle 对象，包含当前活动的样式属性，如 fillColor 和 strokeColor。

以下示例更改项目的当前样式，然后创建继承该样式的路径。 然后它更改 strokeWidth 和 fillColor 并创建另一个路径。

```js
// 更改项目当前的样式：
project.currentStyle = {
	strokeColor: '#000000',
	fillColor: '#ff0000',
	strokeWidth: 3
};

// 路径会继承刚刚设置的样式：
var firstPath = new Path.Circle({
	center: [100, 100],
	radius: 50
});

// 改变项目的当前笔划宽度和填充颜色：
project.currentStyle.strokeWidth = 8;
project.currentStyle.fillColor = 'green';

// 这个路径有 8pt 宽度的笔划和绿色的填充色：
var secondPath = new Path.Circle({
	center: [250, 100],
	radius: 50
});
```

![](/assets/style10.png)

