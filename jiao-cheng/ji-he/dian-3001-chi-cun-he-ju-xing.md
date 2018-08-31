# 点、尺寸和矩形

在 Paper.js 中，[Point](http://paperjs.org/reference/point)，[Size](http://paperjs.org/reference/size) 和 [Rectangle](http://paperjs.org/reference/rectangle) 等基本类型是描述图形项几何属性的对象。它们是几何值的抽象表示，例如位置和尺寸，但不直接表示项目中的图形项。

> **请注意：**
>
> Paper.js 项目中的图形项是显示在图层列表中并在项目中可见的项。可以和现实世界中的“物质”项进行类比。为了描述它们的位置和尺寸，Paper.js 配置了不同的基本类型，这些类型只是描述其几何特性的数值容器。

这意味着当我们在代码中创建一个[Point](http://paperjs.org/reference/point)对象时，我们实际上只是在视图中创建一个位置的描述，但我们不是创建一个包含该点作为段的路径项：

为了创建包含此点作为段的路径项，我们需要显式使用[新的Path（）](http://paperjs.org/reference/path#path)构造函数来创建路径并将该点作为第一个段添加到其中。“[使用路径项”](http://paperjs.org/tutorials/paths/working-with-path-items/)教程更详细地描述了路径和段。

运行此脚本将在Paper.js项目中生成一个“物理”路径项，其中一个段位于myPoint的位置。



#### 请注意：

同样，myPath的“物理”出现段和名为myPoint的点不一样。myPoint只是描述用于生成myPath第一段的坐标。修改myPoint不会在创建后更改该段。

### 点





