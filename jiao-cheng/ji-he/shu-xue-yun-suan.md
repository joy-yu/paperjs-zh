# 数学运算

在 Paper.js 中你可以在基本类型对象上使用普通代数运算符。 点、尺寸可以和数值或其他点、尺寸进行加减乘除：

```js
// 定义一个点：
var point1 = new Point(10, 20);

// 创建第二个点是第一个点的4倍，换一种说法
// 创建一个 x、y 值都是第一个点4倍的点：
var point2 = point1 * 4;
console.log(point2); // { x: 40, y: 80 }

// 现在我们可以计算两点差：
var point3 = point2 - point1;
console.log(point3); // { x: 30, y: 60 }

// 创建另一个点，和 point3 进行数值相加：
var point4 = point3 + 30;
console.log(point4); // { x: 60, y: 90 }

// 三分之一的话会怎么样？
var point5 = point4 / 3;
console.log(point5); // { x: 20, y: 30 }

// 将两个点相乘，就是
// 将两个点的每个坐标分别相乘：
var point6 = point5 * new Point(3, 2);
console.log(point6); // { x: 60, y: 60 }
```

这些运算符完美诠释了[对象转换](http://paperjs.org/tutorials/geometry/object-conversion/)教程中描述的对象转换功能，只要执行操作的对象是真正的 Paper.js 的基本类型：

```js
var point1 = new Point(10, 20);
var point2 = point1 + { x: 100, y: 100 };
console.log(point2); // { x: 110, y: 120 }

// 给 point 添加 size 对象同样生效
// size 对象首先会被强制转化为 point 对象
var point3 = point2 + new Size(50, 100);
console.log(point3); // { x: 160, y: 220 }

// 使用尺寸的对象表示法同样生效:
var point4 = point3 + { width: 40, height: 80 };
console.log(point4); // { x: 200, y: 300 }

// 用数组表示法替代相加会怎么样？同样成功咯~
var point5 = point4 + [100, 0];
console.log(point5); // { x: 300, y: 300 }
```

### 数学函数

Paper.js 提供了几种用于四舍五入 点 和 尺寸 值的数学函数：

```js
var point = new Point(1.2, 1.8);

// 四舍五入：
var rounded = point.round();
console.log(rounded); // { x: 1, y: 2 }

// 向上取整：
var ceiled = point.ceil();
console.log(ceiled); // { x: 2, y: 2 }

// 向下取整：
var floored = point.floor();
console.log(floored); // { x: 1, y: 1 }
```

### 随机值

使用`Point.random()`或`Size.random()`创建一个随机值的 point 或 size，每个属性值为0到1之间的随机值：

```
// 创建一个 point，它的 x 坐标在 0-50 之间
// y 坐标值在 0-100 之间
var point = new Point(50, 100) * Point.random();

// 创建一个 size， 它的宽度在 0-50 之间
// 高度在 0-100 之间
var size = new Size(50, 100) * Size.random();
```



