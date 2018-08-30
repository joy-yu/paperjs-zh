# 特点

Paper.js 基于 Scriptographer 和 HTML5 标准，是一个全面的开源矢量图形脚本框架。

# 文档对象模型

Paper.js 提供了一种非常容易使用的文档对象模型（也称为场景图）。 创建项目并使用图层，组，路径，栅格等等。组和图层可以包含其他物体甚至其他组。

如果你之前从未听说过文档对象模型，您可以将其视为 Adobe Illustrator 和 Adobe Photoshop 等应用程序的图层调色板。

![](/assets/Layers.gif)

上边的图像是执行下面代码后项目结构的图示，你可以在 Adobe Illustrator 这样的应用程序中看到。 它有两层，红色路径在第一层中创建，绿色路径在第二层中创建。

```js
// 创建一个圆形路径，它自动放置在项目的活动层中
var path = new Path.Circle({
    center: [80, 50],
    radius: 35,
    fillColor: 'red'
});

// 创建一个新图层并激活
var secondLayer = new Layer();

// 第二个路径作为第二层的子项添加
var secondPath = new Path.Circle({
    center: [120, 50],
    radius: 35,
    fillColor: '#00FF00'
});
```

在[文档层次结构](http://www.scriptographer.org/tutorials/document-items/document-hierarchy/)教程中可以了解更多相关内容。

# 路径和线段

Paper.js 可以非常轻松地创建路径并为其添加线段。 添加后，可以轻松对其进行查看，操作，移动，移除等操作。

Paper.js中，路径由一系列由曲线连接的线段表示。 一个线段由一个点和两个柄组成，定义了曲线的位置和方向。

在[使用路径项目](http://www.scriptographer.org/tutorials/paths/working-with-path-items/)教程中可以了解更多有关内容。

# 鼠标互动

Paper.js 可以为通过鼠标（或触摸屏）产生的不同行为提供鼠标处理程序。 您可以使用这些处理程序生成不同类型的功能，这些功能可以不同的方式来响应鼠标交互和移动。 你只需在 Paperscript 代码中定义处理函数，这时只要用户与画布交互，它们就会被 Paper.js 调用。

在[创建鼠标工具](http://scriptographer.org/tutorials/interaction/creating-mouse-tools/)教程中可以了解更多相关内容。

```js
function onMouseDown(event) {
    // 当用户鼠标按下时执行代码
}

function onMouseDrag(event) {
    // 当用户拖拽鼠标时执行代码
}

function onMouseUp(event) {
    // 当用户鼠标释放时执行代码
}
```

传递给事件处理程序的事件对象包括许多描述鼠标移动和位置的方便属性。 在[鼠标事件](http://scriptographer.org/tutorials/interaction/mouse-tool-events/)教程中可以了解更多相关内容。

# 键盘互动

Paper.js 你可以通过两种方式与键盘交互：监听按键事件并响应这些事件，或随时检查给定按键的状态，以检查是否按下了键。

在[键盘互动](http://paperjs.org/tutorials/interaction/keyboard-interaction/)教程中可以了解更多相关内容。

```js
function onKeyDown(event) {
    // 当用户按下某一个键时执行代码
}

function onMouseDrag(event) {
    if (Key.isDown('space')) {
        // 鼠标拖拽时，当空格键按下时，执行代码
    }
}
```

下面这个示例显示了一些键盘交互功能。 单击画布以获得键盘焦点并使用箭头键操控：

# SVG 导入/导出

Paper.js提供了非常方便的方法来将矢量图形导入和导出为SVG。 更支持更高级的功能，如渐变和剪裁。

左侧是原始SVG，导入到右侧的 Paper.js 画布中：

这个交互式的 Voronoi 示例很好玩，你可以单击添加新的单位，如果达到你喜欢的结果，你可以点击下载为SVG按钮将结果下载为 SVG 文件，您可以直接在 Adobe Illustrator 和其他矢量编辑应用程序中打开该文件：

# 光栅图像和颜色平均

将图片置入你的项目中，使用该图片的像素颜色或者其顶部的路径像素的平均颜色。

在[图片](http://paperjs.org/tutorials/images/)教程中可以了解更多相关内容。

# 标记

符号允许你在项目中放置物体的多个实例。 这样可以节省内存，因为标记的所有实例都只是引用原始项目，并且它可以加速在复杂对象周围移动，因为内部属性（如线段数组和渐变位置）不需要每次实时转换更新。

# 选择轮廓

当你在代码中选择物体或路径的段点和段柄时，Paper.js 会在项目顶部绘制它们的可视轮廓。 这对于调试非常有用，这样可以查看路径构造，路径曲线的位置，各个分段点以及符号和栅格项的边界框：

```js
var circle = new Path.Circle({
    center: [160, 80],
    radius: 50
});

// 选择路径的第二个线段点
circle.segments[1].selected = true;

// 选择路径的第三个线段点
circle.segments[2].selected = true;

// 在第一个圆右边140像素位置创建第二个圆
var circle2 = new Path.Circle({
    center: circle.position + [140, 0],
    radius: 50,
    fillColor: 'red'
});

// 选择第二个圆
circle2.selected = true;
```

# 矢量几何

Vector几何是 Paper.js 中的一等公民。 在学习编写脚本的同时，了解其基本原理有很大的好处。 毕竟，在“矢量图形”这个词中包含着“矢量”这个词。

在构建 [Scriptographer](http://scriptographer.org/) 时，我们发现矢量几何是一种处理位置、运动和路径的强大方法。一旦理解它，你会发现它比直接使用坐标系的x值和y值更加直观和灵活，就像那些视觉导向的编程环境那样。

在[矢量几何](http://www.scriptographer.org/tutorials/geometry/vector-geometry/)教程中可以了解更多相关内容。

# 数学运算

在 PaperScript 中你可以编写与基本类型对象相关的常规代数运算符。 Points 和 Sizes 可以和数值或其他 Points 和 Sizes 相加减乘数：

```js
// 定义一个点1
var point1 = new Point(10, 20);

// 创建第二点，是第一个点的4倍
// 这和创建一个新的点，x值和y值是第一个点4倍一样
var point2 = point1 * 4;
console.log(point2); // { x: 40, y: 80 }

// 我们可以计算这两个点的差
var point3 = point2 - point1;
console.log(point3); // { x: 30, y: 60 }
```

在[数学运算](http://www.scriptographer.org/tutorials/geometry/mathematical-operations/)教程中可以了解更多相关内容。

# 对象转换

Paper.js 的一个重要特性就是：将值传递给函数时可以进行灵活的参数转换。 在这些情况下，所有基本类型也可以描述为数组或纯 JavaScript 对象。 数组只是一系列标准序列中的默认属性。

```js
// 从 JS 对象创建一个矩形
var rect = new Rectangle({ x: 10, y: 20, width: 100, height: 200 });
console.log(rect); // { x: 10, y: 20, width: 100, height: 200 }

// 以数组形式定义尺寸 [width, height]
rect.size = [200, 300];
console.log(rect); // { x: 10, y: 20, width: 200, height: 300 }

// 从 JS 对象改变矩形的点位置
rect.point = { x: 20, y: 40 };
console.log(rect); // { x: 20, y: 40, width: 200, height: 300 }
```

请注意，在需要的时候，点会被动态转化为尺寸，反之亦然：

```js
var rect = new Rectangle();
rect.point = { width: 100, height: 200 };
console.log(rect); // { x: 100, y: 200, width: 0, height: 0 }

rect.size = { x: 200, y: 400 };
console.log(rect); // { x: 100, y: 200, width: 200, height: 400 }
```



