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
<!-- 定义内联 PaperScript ，将其与 myCanvas 相关联 -->
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
<!-- Load the Paper.js library -->
<script type="text/javascript" src="js/paper.js"></script>
<!-- Load external PaperScript and associate it with myCanvas -->
<script type="text/paperscript" src="js/myScript.js" canvas="myCanvas">
</script>
</head>
<body>
	<canvas id="myCanvas" resize></canvas>
</body>
</html>
```



