# length

只要是数组，就一定有`length`属性。该属性是一个动态的值，等于**键名中的最大整数加上`1`**。

```javascript
var arr = ["a", "b"];
arr.length; // 2

arr[2] = "c";
arr.length; // 3

arr[9] = "d";
arr.length; // 10

arr[1000] = "e";
arr.length; // 1001
```

上面代码表示，数组的数字键不需要连续，`length`属性的值总是比最大的那个**整数键**大`1`。另外，这也表明数组是一种动态的数据结构，可以随时增减数组的成员。

`length`属性是可写的。如果人为设置一个小于当前成员个数的值，该数组的成员数量会**自动减少**到`length`设置的值。

```javascript
var arr = ["a", "b", "c"];
arr.length; // 3

arr.length = 2;
arr; // ["a", "b"]
```

上面代码表示，当数组的`length`属性设为 2（即最大的整数键只能是 1）那么整数键 2（值为`c`）就已经不在数组中了，被自动删除了。

**清空数组的一个有效方法，就是将`length`属性设为 0**。

```javascript
var arr = ["a", "b", "c"];

arr.length = 0;
arr; // []
```

如果人为设置`length`大于当前元素个数，则数组的成员数量会**增加到这个值，新增的位置都是空位**。

```javascript
var a = ["a"];

a.length = 3;
a[1]; // undefined
```

如果人为设置`length`为不合法的值，JavaScript 会报错。

```javascript
// 设置负值
[].length = -1
// RangeError: Invalid array length

// 数组元素个数大于等于2的32次方
[].length = Math.pow(2, 32)
// RangeError: Invalid array length

// 设置字符串
[].length = 'abc'
// RangeError: Invalid array length
```

值得注意的是，由于数组本质上是一种对象，所以可以为数组添加属性，但是这不影响`length`属性的值。

```javascript
var a = [];

a["p"] = "abc";
a.length; // 0

a[2.1] = "abc";
a.length; // 0
```

上面代码将数组的键分别设为字符串和小数，结果都不影响`length`属性。因为，`length`属性的值就是等于**最大的整数键加 1**，而这个数组没有整数键，所以`length`属性保持为`0`。

如果数组的键名是添加**超出范围**的数值，该键名会**自动转为字符串**。

```javascript
var arr = [];
arr[-1] = "a";
arr[Math.pow(2, 32)] = "b";

arr.length; // 0
arr[-1]; // "a"
arr[4294967296]; // "b"
```

上面代码中，我们为数组`arr`添加了两个不合法的数字键，结果`length`属性没有发生变化。这些数字键都变成了字符串键名。最后两行之所以会取到值，是因为取键值时，**数字键名会默认转为字符串**。
