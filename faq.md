# 常见问题

### 我们的项目需要XX功能，你们能实现吗？

如果我们认为这是一个有用的功能，我们会将它添加到我们的[蓝图](http://paperjs.org/about/roadmap/)中。 如果您需要在短期内实现，请与我们联系商讨赞助开发流程。

### 为什么不基于 SVG ?

我们决定使用 Canvas对象 作为主要后端，因为在我们的初始测试中我们发现 Canvas 比 SVG 更快，我们可以优化并完全控制我们自己的场景图/DOM。 SVG导入/导出经过我们的充分测试，是完全可用的。 请参阅下一个问题。

### 如何导出为矢量图形？

2012年11月，paper.js 实现了 SVG 的导入和导出。查看 [project.importSVG\(svg\)](http://paperjs.org/reference/project#importsvg-svg)，[item.importSVG\(svg\)](http://paperjs.org/reference/item#importsvg-svg) / [project.exportSVG\(\)](http://paperjs.org/reference/project#exportsvg)，[item.exportSVG\(\)](http://paperjs.org/reference/item#exportsvg)。在未来，我们可能通过使用额外的库来实现PDF导出功能。

## 会因为使用许多变量而污染全局变量吗？

不用担心，所有 Paper.js 都在自己的作用域范围内编译并存放在全局 [paper](http://paperjs.org/reference/global#paper) 变量中。每个PaperScript 脚本都在自己的作用域范围内运行，执行时它们看上去是在全局作用域，但实际上是在 paper 对象中。 如果您选择不使用 PaperScript 而更喜欢纯JavaScript，那么，你将失去通过简单的数学运算符对 Point 和 Size 对象进行矢量数学运算的额外好处，并且你必须访问 paper 对象上的所有原型。 你可以选择调用 paper.install\(window\) 来污染全局作用域，将所有 Paper.js 原型注入其中，并且无需通过 paper 对象访问所有内容。

### 竞争力如何？不是已经有很多关于Canvas的封装库了？

我们知道现在已经有很多Canvas封装库了，但我们可以看到 Paper.js 远不止于此。 它是一个广泛的库，源于多年的 [Scriptographer](http://scriptographer.org/)  矢量图形和API设计经验。 它提供了许多非常有用的工具来处理 canvas 缺乏的矢量图形：精心设计的场景图和DOM，针对许多贝塞尔曲线相关的高度优化和精确的数学计算，例如边界框计算（有和没有笔画扩展，包括所有不同的笔划样式，甚至斜角限制），曲线和路径长度（使用 Gauss-Legendre 数值积分），路径时间参数化（在给定的偏移/长度下找到贝塞尔参数，使用Newton-Raphson根发现法），曲线拟合和快速路径扁平化，我们可以用近乎原生的速度来实现 Canvas 缺失的虚线功能。

### 为什么为什么不直接使用 HTML5 Canvas？

关于使用 Paper.js 的一系列额外益处，请参阅上一个问题。

### 可以在不编写 PaperScript 的情况下使用 Paper.js 吗？



