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

* A Scene Graph / Document Object Model for vector graphics: Work with nested layers, groups, paths, compound paths, rasters, symbols etc.
* The handling and drawing of these graphic items is automatic and optimised, allowing you to construct or modify your items and styles and leave the drawing commands to Paper.js.
* A well designed and battle hardened Application Programming Interface \(API\).
* PaperScript, a simple extension of JavaScript, allowing the scoped execution of scripts without polluting the global scope, the execution of multiple scripts per page in their separate sand-boxed scopes while sharing the library code, and adding support for operator overloading to any object.
* There is a good reason for the word Vector in Vector Graphics. Paper.js treats Vector Mathematics as a first class citizen by making working with vectors and geometries as simple as possible through its core types such as Point, Size and Rectangle. The manipulation of Point and Size objects is further simplified in PaperScript, where direct math operations using normal operator syntax are possible on such objects as if they were plain numbers.
* Construct paths and manipulate their curves and segments in very convenient and fine-grained ways.
* Inspect and manipulate the precise bounding box of any item, supporting complicated stroke styles with different stroke ends and miter limits.
* Smoothen curves, and simplify path segments by fitting curves through points.
* Simulate dashed strokes which are currently lacking from the Canvas object, at near native drawing speed.
* Most blend modes known from Illustrator and Photoshop supported through emulation in JavaScript: multiply, screen, overlay, soft-light, hard-light, color-dodge, color-burn, darken, lighten, difference, exclusion, hue, saturation, luminosity, color, add, subtract, average & negation.

Read our tutorials to learn more about the features of Paper.js.

