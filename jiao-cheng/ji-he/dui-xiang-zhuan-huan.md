### 对象转换

Paper.js 的一个重要特性是它在将值传递给函数时具有灵活的参数转换能力。 在这些情况下，所有基本类型也可以描述为数组或纯JavaScript 对象。 数组只是标准序列中默认属性的列表。 一些例子：

```js
// 以 JS 对象形式创建一个矩形:
var rect = new Rectangle({ x: 10, y: 20, width: 100, height: 200 });
console.log(rect); // { x: 10, y: 20, width: 100, height: 200 }

// 以数组形式定义尺寸 [width, height]:
rect.size = [200, 300];
console.log(rect); // { x: 10, y: 20, width: 200, height: 300 }

// 通过 JS 对象形式改变矩形的坐标位置:
rect.point = { x: 20, y: 40 };
console.log(rect); // { x: 20, y: 40, width: 200, height: 300 }
```

注意，在需要时，点会动态转换为尺寸，反之亦然：

```js
var rect = new Rectangle();
rect.point = { width: 100, height: 200 };
console.log(rect); // { x: 100, y: 200, width: 0, height: 0 }

rect.size = { x: 200, y: 400 };
console.log(rect); // { x: 100, y: 200, width: 200, height: 400 }
```



