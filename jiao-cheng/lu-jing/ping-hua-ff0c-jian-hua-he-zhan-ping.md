# 平滑，简化和展平

Paper.js提供了两种不同的平滑路径的方法。

`path.smooth()`通过更改其段柄来平滑路径，不添加或删除段点。

`path.simplify()`通过分析 [path.segments](http://paperjs.org/reference/path#segments) 数组并用更优化的段集替换它来平滑路径，从而减少内存使用并加快绘图速度。

### 平滑路径

Paper.js 中你可以使用`path.smooth()`函数自动平滑路径。 这个函数可以计算出路径分段点的柄的最佳值，从而生成平滑经过的曲线。 段不会移动，路径段当前的柄设置会被忽略。

在下面的示例中，我们创建一个矩形路径，创建它的副本对象并平滑副本对象。 如你所见，只有柄的位置发生了变化。 段点保持不变。

```js
var path = new Path({
    segments: [[30, 75], [30, 25], [80, 25], [80, 75]],
    strokeColor: 'black',
    closed: true
});

// 选中路径，从而观察它的柄
path.fullySelected = true;

// 创建一份路径的拷贝，并向右移动100像素
var copy = path.clone();
copy.fullySelected = true;
copy.position.x += 100;

// 平滑路径的段
copy.smooth();
```

![](/assets/smooth1.png)

在下面的视图中单击并拖动以绘制线条，当你释放鼠标时，会使用`path.smooth()`平滑路径：

[例子](http://paperjs.org/tutorials/paths/smoothing-simplifying-flattening/)

### 简化路径

`path.simplify()`通过简化路径来平滑路径。 函数通过分析 [path.segments](http://paperjs.org/reference/path#segments) 数组并用更优化的段集替换它来平滑路径，从而减少内存使用并加快绘图速度。

[例子](#)

`path.simplify()`函数有一个可选的容差参数，它指定允许简化算法偏离原始路径的最大值。 默认情况下，这个值设置为2.5。 把它设置得更低，可以生成更准确的路径，但会有更多的分段点。 把它设置得更高，可以获得更平滑的曲线和更少的分段点，但路径的形状将与原始形状会有些不同。

### 展平路径

`path.flatten(error)`将路径中的曲线转换为具有最大指定偏差数量的直线。 保证结果直线数量不会比 error 参数指定的数量更多。

在下面的示例中，我们创建一个圆形路径并使用`path.flatten(4)`将其拉直：

```js
// 在 { x: 80, y: 50 } 创建一个半径为 35 的圆形路径
var path = new Path.Circle({
	center: [80, 50],
	radius: 35
});

// 选中路径，从而观察它的柄
path.selected = true;

// 创建一份路径的拷贝，并向右移动150像素
var copy = path.clone();
copy.position.x += 150;

// 展平拷贝的路径，最多有4个偏差点:
copy.flatten(4);
```



