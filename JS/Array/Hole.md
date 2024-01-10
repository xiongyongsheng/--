## 数组的空位

当数组的某个位置是空元素，即**两个逗号之间没有任何值**，我们称该数组存在空位（hole）。

```javascript
var a = [1, , 1];
a.length; // 3
```

上面代码表明，**数组的空位不影响**`length`属性。虽然这个位置没有值，引擎依然认为这个位置是**有效的**。

需要注意的是，**如果最后一个元素后面有逗号，并不会产生空位**。也就是说，有没有这个逗号，结果都是一样的。

```javascript
var a = [1, 2, 3];

a.length; // 3
a; // [1, 2, 3]

var b = [, 1, 2, 3];
b.length; // 4
```

上面代码中，数组最后一个成员后面有一个逗号，这不影响`length`属性的值，与没有这个逗号时效果一样。

数组的空位是可以读取的，返回`undefined`。

```javascript
var a = [, , ,];
a[1]; // undefined
```

**使用`delete`命令删除一个数组成员，会形成空位，并且不会影响`length`属性**。

```javascript
var a = [1, 2, 3];
delete a[1];

a[1]; // undefined
a.length; // 3
```

上面代码用`delete`命令删除了数组的第二个元素，这个位置就形成了空位，但是对`length`属性没有影响。也就是说，`length`属性不过滤空位。所以，使用`length`属性进行数组遍历，一定要非常小心。

### 数组的空位不是`undefined`

数组的某个位置是空位，与某个位置是`undefined`，**是不一样的**。如果是空位，使用数组的`forEach`方法、`for...in`结构、以及`Object.keys`方法进行遍历，**空位都会被跳过**。

```javascript
var a = [, , ,];

a.forEach(function (x, i) {
  console.log(i + ". " + x);
});
// 不产生任何输出

for (var i in a) {
  console.log(i);
}
// 不产生任何输出

Object.keys(a);
// []
```

如果某个位置是`undefined`，遍历的时候就**不会被跳过**。

```javascript
var a = [undefined, undefined, undefined];

a.forEach(function (x, i) {
  console.log(i + ". " + x);
});
// 0. undefined
// 1. undefined
// 2. undefined

for (var i in a) {
  console.log(i);
}
// 0
// 1
// 2

Object.keys(a);
// ['0', '1', '2']
```

这就是说，**空位就是数组没有这个元素，所以不会被遍历到**，而`undefined`则表示数组有这个元素，值是`undefined`，所以遍历不会跳过。
