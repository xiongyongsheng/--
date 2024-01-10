## for...in

`for...in`循环不仅可以遍历对象，也可以遍历数组，毕竟数组只是一种特殊对象。

```javascript
var a = [1, 2, 3];

for (var i in a) {
  console.log(a[i]);
}
// 1
// 2
// 3
```

但是，`for...in`不仅会遍历数组所有的数字键，**还会遍历非数字键**。

```javascript
var a = [1, 2, 3];
a.foo = true;

for (var key in a) {
  console.log(key);
}
// 0
// 1
// 2
// foo
```

上面代码在遍历数组时，也遍历到了非整数键`foo`。所以，**不推荐**使用`for...in`遍历数组。

数组的遍历可以考虑使用`for`循环或`while`循环。
