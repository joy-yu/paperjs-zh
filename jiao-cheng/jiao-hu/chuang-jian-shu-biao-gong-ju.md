# 创建鼠标工具

本教程介绍了创建 Paper.js 工具的不同方法，从而使用户可以通过鼠标进行交互。

### 我的第一个鼠标工具

我们从一个非常简单的工具示例开始，它在脚本执行时会创建一个空路径，并在你单击鼠标时给路径添加段：

```js
// 脚本执行时，立即创建一个新路径
var myPath = new Path();
myPath.strokeColor = 'black';

// 当用户在视图中点击鼠标时，函数会立刻被调用
function onMouseDown(event) {
    // 在鼠标位置处给路径添加一个段：
    myPath.add(event.point);
}
```

### 鼠标处理函数

Paper.js 可以为通过鼠标产生的不同行为提供鼠标处理程序。你可以使用这些鼠标处理程序生成不同类型的工具，这些工具有不同的方式来响应鼠标交互和移动。

> **请注意：**
>
> 在JavaScript中，函数是代码块，写在其它 script 区域时只有调用它们时才会执行。 处理函数是在某个事件发生时由 Paper.js 调用的函数。

要查看何时调用了这些不同的处理函数，请将以下代码复制粘贴到新的 JavaScript 文件中，执行它并与 Paper.js 工具交互：

```js
function onMouseDown(event) {
    console.log('You pressed the mouse!');
}

function onMouseDrag(event) {
    console.log('You dragged the mouse!');
}

function onMouseUp(event) {
    console.log('You released the mouse!');
}
```

### 事件对象

鼠标处理函数接收一个事件对象，其中包含有关鼠标事件的信息，例如鼠标的当前位置（event.point），按下鼠标的位置（event.downPoint），鼠标事件的压力（ event.pressure）等等。

> **你知道吗？**
>
> [鼠标工具事件](http://paperjs.org/tutorials/interaction/mouse-tool-events/)教程中详细介绍了事件对象的属性。

### 线条工具示例

这是一个绘制线条的简单工具。线条的起点是你单击时的位置，最后一个点是你释放鼠标时的位置。

试着在下面点击，拖动和释放：

```js
// 定义一个空变量，使两个鼠标处理函数都能访问到
var myPath;

function onMouseDown(event) {
	// 鼠标按下时，给 myPath 创建一个新路径
	// 给路径的第一个段设置坐标位置和黑色笔划
	myPath = new Path();
	myPath.strokeColor = 'black';
	myPath.add(event.point);
}

function onMouseUp(event) {
	// 鼠标释放时，给线条的最后一个段设置新的坐标位置
	myPath.add(event.point);
}
```

> **请注意：**
>
> 这个工具与第一个示例之间的区别在于，每次单击鼠标时都会创建一个新路径，并在释放鼠标时结束路径。



