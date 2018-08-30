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

在[文档层次结构](http://www.scriptographer.org/tutorials/document-items/document-hierarchy/)教程中可以了解更多有关文档对象模型的内容。

# 路径和线段

Paper.js 可以非常轻松地创建路径并为其添加线段。 添加后，可以轻松对其进行查看，操作，移动，移除等操作。

Paper.js中，路径由一系列由曲线连接的线段表示。 一个线段由一个点和两个柄组成，定义了曲线的位置和方向。

在[使用路径项目](http://www.scriptographer.org/tutorials/paths/working-with-path-items/)教程中可以了解更多有关路径和段的内容。

# 鼠标互动

Paper.js 可以为通过鼠标（或触摸屏）产生的不同行为提供鼠标处理程序。 您可以使用这些处理程序生成不同类型的功能，这些功能可以不同的方式来响应鼠标交互和移动。 你只需在 Paperscript 代码中定义处理函数，这时只要用户与画布交互，它们就会被 Paper.js 调用。

在[创建鼠标工具](http://scriptographer.org/tutorials/interaction/creating-mouse-tools/)教程中可以了解更多有关鼠标处理程序的内容。

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

传递给事件处理程序的事件对象包括许多描述鼠标移动和位置的方便属性。 在[鼠标事件](http://scriptographer.org/tutorials/interaction/mouse-tool-events/)教程中可以了解更多有关鼠标事件的内容。

# 键盘互动

Paper.js 你可以通过两种方式与键盘交互：监听按键事件并响应这些事件，或随时检查给定按键的状态，以检查是否按下了键。

在[键盘互动](http://paperjs.org/tutorials/interaction/keyboard-interaction/)教程中可以了解更多有关键盘互动的内容。

```js
function onKeyDown(event) {
	// 当用户按下某一个键时执行代码
}

function onMouseDrag(event) {
	if (Key.isDown('space')) {
		// Do something if the space bar is pressed
		// while dragging:
	}
}
```

# SVG 导入/导出

# 光栅图像和颜色平均

# 标记

# 选择轮廓

# 矢量几何

# 数学运算

# 对象转换



