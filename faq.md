# 常见问题

### 我们的项目需要XX功能，你们能实现吗？

如果我们认为这是一个有用的功能，我们会将它添加到我们的[蓝图](http://paperjs.org/about/roadmap/)中。 如果您需要在短期内实现，请与我们联系商讨赞助开发流程。

### 为什么不基于 SVG ?

我们决定使用 Canvas对象 作为主要后端，因为在我们的初始测试中我们发现 Canvas 比 SVG 更快，我们可以优化并完全控制我们自己的场景图/DOM。 SVG导入/导出经过我们的充分测试，是完全可用的。 请参阅下一个问题。

### 如何导出为矢量图形？

2012年11月，paper.js 实现了 SVG 的导入和导出。查看 [project.importSVG\(svg\)](http://paperjs.org/reference/project#importsvg-svg)，[item.importSVG\(svg\)](http://paperjs.org/reference/item#importsvg-svg) / [project.exportSVG\(\)](http://paperjs.org/reference/project#exportsvg)，[item.exportSVG\(\)](http://paperjs.org/reference/item#exportsvg)。在未来，我们可能以额外的库，来有望实现PDF导出。

## 会因为使用许多变量而污染全局变量吗？

不用担心，所有 Paper.js 都在自己的作用域范围内编译并存放在全局 [paper](http://paperjs.org/reference/global#paper) 变量中。每个PaperScript 脚本都在自己的作用域范围内运行，执行时它们看上去是在全局作用域，但实际上是在 paper 对象。 如果您选择不使用 PaperScript 而更喜欢纯JavaScript，那么，你将失去通过简单的数学运算符对 Point 和 Size 对象进行矢量数学运算的额外好处，并且您必须访问此纸质对象上的所有原型。 您可以选择通过调用paper.install（窗口）来污染全局范围，将所有Paper.js原型注入其中，并且无需通过纸质对象访问所有内容。

