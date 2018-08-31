# 使用 Paper.js

Paper.js 为浏览器的集成提供了不同的方法。 最简单的方法是使用 PaperScript，那是我们的 JavaScript 扩展，它可以在开发过程中帮助你完成一些事情。 对于更多高级用户或更大的项目，最好直接使用 JavaScript，可以在这里查看[直接使用 JavaScript](http://paperjs.org/tutorials/getting-started/using-javascript-directly/) 。

### 什么是 PaperScript ?

PaperScript 是普通的 JavaScript，同时增加了对 [Point](http://paperjs.org/reference/point) 和 [Size](http://paperjs.org/reference/size) 对象的数学运算符（+ - \* /％）的支持。 PaperScript 代码在其自己的作用域范围内自动执行，不受全局作用域污染仍然可以访问所有全局浏览器对象和函数，例如 document 或 window。

默认情况下，Paper.js 库仅将一个对象导出到全局范围：**paper** 对象。 它包含库定义的所有类和对象。 使用 PaperScript 时，用户不需要关心这一点，因为在 PaperScript 代码中，通过使用巧妙的作用域范围，所有 paper 对象和函数看起来都是全局的。

PaperScript 还提供自动创建 Project，View 和鼠标 Tool 对象，并简化这些事件处理程序的安装。

### 脚本配置

PaperScript 代码的加载方式与JavaScript中使用 &lt;script&gt;标签 加载其它脚本的方式一样，但是 type 需要设置为“text/paperscript”或“text/x-paperscript”类型。 代码可以是外部文件（src =“URL”），也可以是内联文件：

```html
<!DOCTYPE html>
<html>
<head>
<!-- 加载 Paper.js 库 -->
<script type="text/javascript" src="js/paper.js"></script>
<!-- 定义内联 PaperScript，将其与 myCanvas 相关联 -->
<script type="text/paperscript" canvas="myCanvas">
    // 创建 Paper.js 路径，在其中绘制线条：
    var path = new Path();
    // 给笔画一种颜色
    path.strokeColor = 'black';
    var start = new Point(100, 100);
    // 移动到开始位并从那开始画一条线
    path.moveTo(start);
    // 注意 Point 对象上的加号运算符。
    // PaperScript 为我们做了这些，还有更多！
    path.lineTo(start + [ 100, -50 ]);
</script>
</head>
<body>
    <canvas id="myCanvas" resize></canvas>
</body>
</html>
```

如果我们将内联代码复制到名为`js/myScript.js`的文件中，我们可以重写上面的示例来加载外部文件。

```html
<!DOCTYPE html>
<html>
<head>
<!-- 加载 Paper.js 库 -->
<script type="text/javascript" src="js/paper.js"></script>
<!-- 加载外部 PaperScript，将其与 myCanvas 相关联 -->
<script type="text/paperscript" src="js/myScript.js" canvas="myCanvas"></script>
</head>
<body>
    <canvas id="myCanvas" resize></canvas>
</body>
</html>
```

PaperScript 的 &lt;script&gt; 标签支持以下这些属性：

**src="URL"**：加载 PaperScript 代码的 URL。

**canvas="ID"**：将 PaperScript 代码关联到指定 ID 的 canvas，并为其生成 [Project](http://paperjs.org/reference/project) 和 [View](http://paperjs.org/reference/view) 对象。 如果你想验证，`data-paper-canvas="ID"`同样有效。

> **请注意：**
>
> 当页面包含多个 PaperScript 时，每个脚本将在它自己的作用域范围内运行，而且无法访问在其他脚本中声明的对象和函数。
>
> 如果想让 PaperScript 与其他 PaperScript 或 JavaScript 代码进行通信，请参阅 [PaperScript 互用性](http://paperjs.org/tutorials/getting-started/paperscript-interoperability/)教程。

### Canvas 配置

我们可以通过向 canvas 标签添加属性，来配置 Paper.js：

**resize="true"**：使 canvas 对象与浏览器窗口的宽高一样，并在用户调整浏览器窗口大小时自动调整 canvas 大小。 调整窗口大小时，global.view 的大小也会自动调整。如果你想验证，`data-paper-resize="true"`同样有效。

你可以通过在代码中编写 onResize 处理函数来响应窗口的任何大小调整行为。 例如，假设你在视图的中心创建一个圆形路径，并且你希望它在调整大小后依旧居中：

```js
// 创建一个圆形路径，它的圆心在视图中心，半径为30:
var path = new Path.Circle({
    center: view.center,
    radius: 30,
    strokeColor: 'black'
});

function onResize(event) {
    // 当窗口调整时，使路径重新居中:
    path.position = view.center;
}
```

**hidpi="off"**：默认情况下，Paper.js 在 Hi-DPI（Retina）屏幕上渲染高分辨率 canvas 以匹配屏幕的原始分辨率，并为你显式地处理所有其他变换。如果你不想这么做，想降低内存占用或提高渲染性能，可以通过在 canvas 标签中设置 `hidpi="off"` 来关闭它。 如果你想验证，`data-paper-hidpi="off"`同样有效。

