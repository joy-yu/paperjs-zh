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

这些运算符与对象转换教程中描述的对象转换功能一起工作得很好，只要执行操作的对象是真正的基本类型：

```js
var point1 = new Point(10, 20);
var point2 = point1 + { x: 100, y: 100 };
console.log(point2); // { x: 110, y: 120 }

// Adding size objects to points work too,
// forcing them to be converted to a point first
var point3 = point2 + new Size(50, 100);
console.log(point3); // { x: 160, y: 220 }

// And using the object notation for size works just as well:
var point4 = point3 + { width: 40, height: 80 };
console.log(point4); // { x: 200, y: 300 }

// How about adding a point in array notation instead?
var point5 = point4 + [100, 0];
console.log(point5); // { x: 300, y: 300 }
```



