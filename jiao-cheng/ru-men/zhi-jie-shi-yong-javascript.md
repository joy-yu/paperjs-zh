# 直接使用 JavaScript

### Paper.js 架构

为了理解如何直接从 JavaScript 使用 Paper.js，而不使用 PaperScript 自动机制，我们首先需要解释一下 Paper.js 的架构。使用PaperScript 时，每个脚本都在自己的作用域范围内运行，即 [PaperScope](http://paperjs.org/reference/paperscope) 对象。库提供的全局 [paper](http://paperjs.org/reference/global#paper) 对象也是 [PaperScope](http://paperjs.org/reference/paperscope) 对象。这样有助于我们理解 将作用域视为执行上下文 的概念。

引入作用域是为了让页面上的多个示例具有单独的 PaperScript 上下文，每个示例都有自己的视图和项目，共享同一份库的代码，但是彼此无法访问。它们可以被视为带有共享代码的沙盒“插件”。

每个作用域或上下文都包含一些描述其状态的对象，例如开放的 [projects](http://paperjs.org/reference/paperscope#projects) 列表，活动 [project](http://paperjs.org/reference/paperscope#project) 的引用，代表 canvas 元素的 [views](http://paperjs.org/reference/paperscope#views) 列表，当前活动的 [view](http://paperjs.org/reference/paperscope#views)，鼠标 [tools](http://paperjs.org/reference/paperscope#tools) 列表，当前活动的 [tool](http://paperjs.org/reference/paperscope#tool) 等。

我们来解释一下作用域，项目，视图和工具之间的关系：每个作用域可以包含一个或多个项目，这些项目通过一个或多个视图显示（每个视图代表一个 Paper.js canvas）。视图与具体项目无关，事实上视图渲染了可见区域内具有物体项的所有可见项目。工具可以在任意视图中的任意项目上使用，只要它们属于同一作用域。

### 设置作用域

直接使用 JavaScript 时，大多数情况下，只需要一个作用域即可。 在这个作用域内，可以通过 [new Project\(\)](http://paperjs.org/reference/project#project) 和 [new View\(canvas\)](http://paperjs.org/reference/view#view-canvas) 构造函数创建多个项目或视图。

最简单的方法是使用现有的纸质对象，并使用其paperScope.setup（canvas）方法为我们初始化一个空项目和一个视图。 我们重用了Working with Paper.js中的示例，以便了解直接使用JavaScript时还需要什么：

```html
<!DOCTYPE html>
<html>
<head>
<!-- Load the Paper.js library -->
<script type="text/javascript" src="js/paper.js"></script>
<!-- Define inlined JavaScript -->
<script type="text/javascript">
	// Only executed our code once the DOM is ready.
	window.onload = function() {
		// Get a reference to the canvas object
		var canvas = document.getElementById('myCanvas');
		// Create an empty project and a view for the canvas:
		paper.setup(canvas);
		// Create a Paper.js Path to draw a line into it:
		var path = new paper.Path();
		// Give the stroke a color
		path.strokeColor = 'black';
		var start = new paper.Point(100, 100);
		// Move to start and draw a line from there
		path.moveTo(start);
		// Note that the plus operator on Point objects does not work
		// in JavaScript. Instead, we need to call the add() function:
		path.lineTo(start.add([ 200, -50 ]));
		// Draw the view now:
		paper.view.draw();
	}
</script>
</head>
<body>
	<canvas id="myCanvas" resize></canvas>
</body>
</html>
```



