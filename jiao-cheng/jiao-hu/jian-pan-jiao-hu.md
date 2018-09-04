# 键盘交互

Paper.js 中你能以两种方式与键盘进行交互：你可以监听按键事件并响应这些事件，或者你可以随时检查指定键的状态，以检查是否按下了键。本教程具体解释了这两种方法。

### 接收按键事件

要获取有关按键的信息，请在脚本中定义`onKeyDown`或`onKeyUp`处理函数。

下面的示例中，我们通过创建文本项并修改内容，来给用户提供哪个键被按下/释放的反馈：

```js
// 在视图中心创建一个居中的文本项：
var text = new PointText({
	point: view.center,
	content: 'Click here to focus and then press some keys.',
	justification: 'center',
	fontSize: 15
});

function onKeyDown(event) {
	// 当键被按下，设置文本项的内容：
	text.content = 'The ' + event.key + ' key was pressed!';
}

function onKeyUp(event) {
	// 当键释放，设置文本项的内容：
	text.content = 'The ' + event.key + ' key was released!';
}
```

> **请注意：**
>
> 按住键时会连续触发 onKeyDown 事件。

### 事件对象

上面的示例使用 event.key 属性来查看按下了哪个键。 事件对象包含几个描述按键事件的属性：

event.key：按下的键。

event.character：按键生成的字符。 例如，当按下 shift 和 a 时，将显示大写的 A。

event.type：按键事件的类型，'keydown' 或 'keyup'。

### 检查按键是否按下

要检查当前是否按下了某个键，我们可以使用`Key.isDown(key)`函数。

下面的示例中，我们创建一个路径，并在用户拖动鼠标时向路径添加段。 当拖动时按下 'a' 键，我们将最后添加的段移到鼠标的位置，而不是添加新的段。

```js
var path;
function onMouseDown(event) {
	path = new Path();
	path.strokeColor = 'black';
	path.add(event.point);
}

function onMouseDrag(event) {
	if(Key.isDown('a')) {
		// 如果 'a' 键按下，
		// 移动最后一个段点到鼠标的位置：
		path.lastSegment.point = event.point;
	} else {
		// 如果键没被按下，在鼠标的位置添加一个段：
		path.add(event.point);
	}
}
```

### 辅助按键

传递给鼠标事件处理程序（如 onMouseDown）的事件对象还包含有关按下哪些辅助按键的信息。 辅助按键是不直接产生字符的键：capsLock，command，control，option，shift。

event.modifiers 属性是一个对象，提供不同辅助按键的布尔值。 例如，要检查 shift 键是否关闭，您可以执行以下操作：

```js
function onMouseDrag(event) {
	if (event.modifiers.shift) {
		// 当 shift 键按下时执行某些操作
	}
}
```

例如，如果我们想使用 shift 键，达到和上面示例脚本的相同效果：

```js
var path;
function onMouseDown(event) {
	path = new Path();
	path.strokeColor = 'black';
	path.add(event.point, event.point);
}

function onMouseDrag(event) {
	if(event.modifiers.shift) {
		// 如果 'shift' 键按下，
		// 移动最后一个段点到鼠标的位置：
		path.lastSegment.point = event.point;
	} else {
		// 如果键没被按下，在鼠标的位置添加一个段：
		path.add(event.point);
	}
}
```

### 享受按键的乐趣

以下示例会在运行时创建路径，并在按下 **wasd** 中的一个键时在对应按键方向上给路径添加段点。

单击下面的视图，使其获得键盘焦点并按下 wasd 中的一个键。

```js
//线的起始点
var position = new Point(100, 100);

// 当键按下时移动的距离：
var step = 10;

var path = new Path();
path.strokeColor = 'black';
path.add(position);

function onKeyDown(event) {
	if(event.key == 'a') {
		position.x -= step;
	}

	if(event.key == 'd') {
		position.x += step;
	}

	if(event.key == 'w') {
		position.y -= step;
	}

	if(event.key == 's') {
		position.y += step;
	}
	path.add(position);
}
```



