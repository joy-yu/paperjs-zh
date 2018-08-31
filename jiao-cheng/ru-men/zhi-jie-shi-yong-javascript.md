# 直接使用 JavaScript

### Paper.js 架构

为了理解如何直接从 JavaScript 使用 Paper.js，而不使用 PaperScript 自动机制，我们首先需要解释一下 Paper.js 的架构。使用PaperScript 时，每个脚本都在自己的作用域范围内运行，即 [PaperScope](http://paperjs.org/reference/paperscope) 对象。库提供的全局 [paper](http://paperjs.org/reference/global#paper) 对象也是 [PaperScope](http://paperjs.org/reference/paperscope) 对象。这样有助于我们理解 将作用域视为执行上下文 的概念。

引入作用域是为了让页面上的多个示例具有单独的 PaperScript 上下文，每个示例都有自己的视图和项目，共享同一份库的代码，但是彼此无法访问。它们可以被视为带有共享代码的沙盒“插件”。

每个作用域或上下文都包含一些描述其状态的对象，例如开放的 [projects](http://paperjs.org/reference/paperscope#projects) 列表，活动 [project](http://paperjs.org/reference/paperscope#project) 的引用，代表 canvas 元素的 [views](http://paperjs.org/reference/paperscope#views) 列表，当前活动的 [view](http://paperjs.org/reference/paperscope#views)，鼠标 [tools](http://paperjs.org/reference/paperscope#tools) 列表，当前活动的 [tool](http://paperjs.org/reference/paperscope#tool) 等。

我们来解释一下作用域，项目，视图和工具之间的关系：每个作用域可以包含一个或多个项目，这些项目通过一个或多个视图显示（每个视图代表一个 Paper.js 画布）。视图与特定项目无关，但实际上渲染了可见区域内具有项目的所有可见项目。工具可以在任何视图中的任何项目上工作，只要它们属于同一范围。

