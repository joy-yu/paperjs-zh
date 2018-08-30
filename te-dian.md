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

[文档层次结构](http://www.scriptographer.org/tutorials/document-items/document-hierarchy/)教程可以了解更多有关文档对象模型的内容。

# 路径和线段

Paper.js 可以非常轻松地创建路径并为其添加线段。 添加后，可以轻松对其进行查看，操作，移动，移除等操作。

Paper.js中，路径由一系列由曲线连接的线段表示。 一个线段由一个点和两个柄组成，定义了曲线的位置和方向。

[使用路径项目](http://www.scriptographer.org/tutorials/paths/working-with-path-items/)教程可以了解更多有关路径和段的内容。

# 鼠标互动

# 键盘互动

# SVG 导入/导出

# 光栅图像和颜色平均

# 标记

# 选择轮廓

# 矢量几何

# 数学运算

# 对象转换



