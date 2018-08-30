# 关于

Paper.js — 矢量图形脚本的瑞士军刀。

![](/assets/paper-js.gif)

Paper.js 是一个开源的基于 HTML5 Canvas 运行的矢量图形脚本框架。 它提供了清晰的场景图/DOM，同时拥有许多强大的功能来创建和使用矢量图形和贝塞尔曲线，所有这些都被巧妙地包含在一个设计良好，干净一致的编程接口中。

![](/assets/scriptographer.jpg)

Paper.js 基于 [Scriptographer](http://scriptographer.org/)，并且很大程度上兼容 [Scriptographer](http://scriptographer.org/)，[Scriptographer](http://scriptographer.org/) 是 Adobe Illustrator 的脚本环境，它拥有一个活跃的开发者社区，并且有十几年的发展。

Paper.js 简单易学，适合初学者，对许多中高级用户的学习也有很多帮助。

Paper.js 由 [Jürg Lehni](http://lehni.org/) 和 [Jonathan Puckey](http://jonathanpuckey.com/) 开发完成，发布遵从[MIT协议](http://paperjs.org/license/)。

# 入门

* 首先，我们可以看看一些[示例](http://paperjs.org/examples/)。
* [下载](http://paperjs.org/download/) Paper.js，或者从[Github 仓库](http://github.com/paperjs/paper.js)查看最新版本。
* 想学习 Paper.js？ 从我们的[教程](http://paperjs.org/tutorials/)开始。
* 如果你有任何的问题或意见，可以加入我们的[邮件列表](http://groups.google.com/group/paperjs)。
* 想及时了解最新信息，可以关注我们的[Twitter](http://twitter.com/paperjs)。

# 总览

Paper.js不仅仅是Canvas的包装器，它提供了更多功能：

* 矢量图形的场景图/DOM：使用嵌套图层\(nested layers\)、组\(groups\)、路径\(paths\)、复合路径\(compound paths\)、 栅格\(rasters\)、 标记\(symbols\)等等。
* 图形项目的处理和绘制是自动的并且经过优化，你可以构建或修改你的项目和样式，并将绘图命令交给Paper.js处理。
* 精心设计并经过千锤百炼的API。
* PaperScript，是 JavaScript 的扩展，允许脚本的局部作用域执行而不会污染全局作用域，共享同一个库的代码时，每个页面的多个脚本可以在它单独的作用域内执行，并添加了对任意对象的运算符重载支持。
* 很好地解释了矢量图形中的矢量。Paper.js 将矢量数学视为一等公民，它通过其核心类型（如Point、Size和Rectangle）尽可能简单地处理矢量和几何图形。PaperScript 进一步简化了对 Point 和 Size 对象的操作，可以使用常规的运算符语法在这些对象上进行直接的数学运算，就像它们是纯数字一样。
* 可以构建路径并以非常方便和精细的方式控制它们的曲线\(curves\)和段\(segments\)。
* 可以查看并控制任何项目的精确边界框，支持的不同笔划端和斜接限制的复杂笔划样式。 
* 平滑曲线，并通过点拟合曲线来简化路径段。
* 模拟当前Canvas对象缺少的虚线笔划，接近原生绘图速度。
* 通过 JavaScript 的模拟支持 Illustrator 和 Photoshop 中的大多数混合模式：正片叠底，滤色，叠加，柔光，强光，颜色减淡，颜色燃烧，变暗，变亮，差异，排斥，色调，饱和度，亮度， 颜色，加，减，平均和否定。multiply, screen, overlay, soft-light, hard-light, color-dodge, color-burn, darken, lighten, difference, exclusion, hue, saturation, luminosity, color, add, subtract, average & negation.

Read our tutorials to learn more about the features of Paper.js.

# 浏览器支持

Paper.js 主要面向支持Canvas对象和EcmaScript 5的现代浏览器。尽管理论上可以编写代码来支持旧版浏览器（IE8及以下版本，我们期待你的加入！），但我们目前还不支持那些旧浏览器，让我们继续前进吧！

