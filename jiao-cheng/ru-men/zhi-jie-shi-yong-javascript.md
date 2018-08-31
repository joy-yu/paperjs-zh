# 直接使用 JavaScript

### Paper.js 架构

为了理解如何直接从 JavaScript 使用 Paper.js，而不使用 PaperScript 自动机制，我们首先需要解释一下 Paper.js 的架构。使用PaperScript 时，每个脚本都在自己的作用域范围内运行，即 [PaperScope](http://paperjs.org/reference/paperscope) 对象。库提供的全局 [paper](http://paperjs.org/reference/global#paper) 对象也是 [PaperScope](http://paperjs.org/reference/paperscope) 对象。这样有助于我们理解 将作用域视为执行上下文 的概念。

引入作用域是为了让页面上的多个示例具有单独的 PaperScript 上下文，每个示例都有自己的视图和项目，共享同一份库的代码，但是彼此无法访问。它们可以被视为带有共享代码的沙盒“插件”。

每个作用域或上下文都包含一些描述其状态的对象，例如开放的 [projects](http://paperjs.org/reference/paperscope#projects) 列表，活动 [project](http://paperjs.org/reference/paperscope#project) 的引用，代表 canvas 元素的 [views](http://paperjs.org/reference/paperscope#views) 列表，当前活动的 [view](http://paperjs.org/reference/paperscope#views)，鼠标 [tools](http://paperjs.org/reference/paperscope#tools) 列表，当前活动的 [tool](http://paperjs.org/reference/paperscope#tool) 等。

我们来解释一下作用域，项目，视图和工具之间的关系：每个作用域可以包含一个或多个项目，这些项目通过一个或多个视图显示（每个视图代表一个 Paper.js canvas）。视图与具体项目无关，事实上视图渲染了可见区域内具有物体项的所有可见项目。工具可以在任意视图中的任意项目上使用，只要它们属于同一作用域。

### 设置作用域

直接使用 JavaScript 时，大多数情况下，只需要一个作用域即可。 在这个作用域内，可以通过 [new Project\(\)](http://paperjs.org/reference/project#project) 和 [new View\(canvas\)](http://paperjs.org/reference/view#view-canvas) 构造函数创建多个项目或视图。

最简单的方法是使用现有的 [paper](http://paperjs.org/reference/global#paper) 对象，并使用它的 [paperScope.setup\(canvas\)](http://paperjs.org/reference/paperscope#setup-canvas) 方法为我们初始化空项目和视图。 我们复用了[使用 Paper.js](http://paperjs.org/tutorials/getting-started/working-with-paper-js/)中的示例，以便了解直接使用 JavaScript 时还需要什么：

```html
<!DOCTYPE html>
<html>
<head>
<!-- 加载 Paper.js 库 -->
<script type="text/javascript" src="js/paper.js"></script>
<!-- 定义内联 JavaScript -->
<script type="text/javascript">
    // 当 DOM 渲染完毕时执行代码
    window.onload = function() {
        // 获取 canvas 对象的引用
        var canvas = document.getElementById('myCanvas');
        // 为 canvas 创建一个空项目和视图:
        paper.setup(canvas);
        // 创建一个 Paper.js 路径 在其中绘制线条:
        var path = new paper.Path();
        // 给画笔上色
        path.strokeColor = 'black';
        var start = new paper.Point(100, 100);
        // 移动到起始点并从那开始画线
        path.moveTo(start);
        // 注意 Point 对象上的加法运算在 JavaScript 中不再有效
        // 我们需要调用 add() 函数:
        path.lineTo(start.add([ 200, -50 ]));
        // 绘制视图:
        paper.view.draw();
    }
</script>
</head>
<body>
    <canvas id="myCanvas" resize></canvas>
</body>
</html>
```

到此为止，如果我们将这个示例与 PaperScript 中编写的示例进行比较，我们会发现一些差异。 除了上面示例中的代码之外，我们还需要：

* 在 DOM 加载完毕时注册处理程序，在此之前我们无法使用 canvas。
* 告诉 paper 对象为 canvas 设置 Project 和  View。 除了传递 canvas 对象，我们也可以将 canvas 元素的 ID 作为字符串传递给 paper 对象。 在 PaperScript 中，会通过`canvas ="ID"`属性自动绑定。
* 通过 paper 对象访问所有 Paper.js 的类和对象，因为它们不再是全局的。
* 在 Point 和 Size 对象上使用数学函数而不是运算符。
* 最后绘制视图，因为现在只有在设置了 [view.onFrame](http://paperjs.org/reference/view#onframe) 处理函数时才会自动绘制。

> **请注意：**
>
> **教程** 和 **引用** 中的所有示例都假设你使用的是 PaperScript。 如果你直接使用 JavaScript，需要牢记这些差异。
>
> **请注意：**
>
> 在上面的代码中，我们使用 window.onload = handler 来获取 DOM 加载完毕时的回调。如果你正在使用诸如 jQuery 之类的框架，则可以使用 $\(document\).ready\(handler\) 来注册 DOM-Ready 事件，该事件在 onload 事件之前触发。

### 作用域全局化

通过 paper 对象访问所有的类和对象可能不太方便，因此这里有两种策略来规避它。

最直接的方法是将 paper 对象的所有字段复制到全局范围。我们可以手动完成，如果只有一个 project，view 和 tool，这样很有效。 但是，如果有多个，对活动的（project，view 和 tool）的全局引用将不会保持最新状态。 幸运的是，我们可以在内部执行一些 JavaScript 技巧，以保持引用同步：paper.install\(window\)。 这样我们可以重写上面例子的代码：

```js
// 通过把 paper 注入到 window，使 paper 作用域全局化:
paper.install(window);
window.onload = function() {
    // 直接从 canvas 的 id 设置:
    paper.setup('myCanvas');
    var path = new Path();
    path.strokeColor = 'black';
    var start = new Point(100, 100);
    path.moveTo(start);
    path.lineTo(start.add([ 200, -50 ]));
    view.draw();
}
```

如果觉得污染全局作用域不是很好的选择，那么第二种策略是通过使用可怕的`with()`语句来绕过它。 这是Paper.js 在内部应用的一个小技巧，用来在它自己的 PaperScope 对象中确定 PaperScript 的作用域：

```js
window.onload = function() {
    paper.setup('myCanvas');
    with (paper) {
        var path = new Path();
        path.strokeColor = 'black';
        var start = new Point(100, 100);
        path.moveTo(start);
        path.lineTo(start.add([ 200, -50 ]));
        view.draw();
    }
}
```

### 设置事件处理程序

PaperScript 在声明为全局函数时会辨识几个特殊事件处理程序，而在 JavaScript 中，需要手动将这些处理程序配置在对应的对象上。 这两个处理程序是 [onFrame](http://paperjs.org/reference/view#onframe) 和 [onResize](http://paperjs.org/reference/view#onresize)，它们都属于 View 类。 如上例所示，如果我们使用 [paperScope.setup\(canvas\)](http://paperjs.org/reference/paperscope#setup-canvas) 函数，就会自动为我们创建 view。 所以我们要做的就是在现有的 view 对象上设置这些处理程序：

```html
<!DOCTYPE html>
<html>
<head>
<script type="text/javascript" src="js/paper.js"></script>
<script type="text/javascript">
    paper.install(window);
    window.onload = function() {
        paper.setup('myCanvas');
        var path = new Path.Rectangle([75, 75], [100, 100]);
        path.strokeColor = 'black';

        view.onFrame = function(event) {
            // 每一帧时，路径旋转3度:
            path.rotate(3);
        }
    }
</script>
</head>
<body>
    <canvas id="myCanvas" resize></canvas>
</body>
</html>
```

> **你知道吗？**
>
> 您可以在教程[创建动画](http://paperjs.org/tutorials/animation/creating-animations/)中阅读有关动画的更多信息。

### 使用工具

就像使用视图处理程序一样，PaperScript 通过使工具处理程序看起来像是全局的来简化和隐藏对 Tool 对象的处理，并且，如果存在这些处理程序如：onMouseDown，onMouseUp，onMouseDrag，onMouseMove 等等，则会为我们动态创建一个 tool。

在 JavaScript 中，我们需要自己创建工具，手动给它们设置处理程序。 这种方法的优点是更加清晰，多个 tool 的处理程序也再正常不过。

```html
<!DOCTYPE html>
<html>
<head>
<script type="text/javascript" src="js/paper.js"></script>
<script type="text/javascript">
    paper.install(window);
    window.onload = function() {
        paper.setup('myCanvas');
        // 创建一个简单的绘画工具:
        var tool = new Tool();
        var path;

        // 定义一个 mousedown 和 mousedrag 处理程序
        tool.onMouseDown = function(event) {
            path = new Path();
            path.strokeColor = 'black';
            path.add(event.point);
        }

        tool.onMouseDrag = function(event) {
            path.add(event.point);
        }
    }
</script>
</head>
<body>
    <canvas id="myCanvas" resize></canvas>
</body>
</html>
```



