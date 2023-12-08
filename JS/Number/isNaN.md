# isNaN

`isNaN` 只对数值有效，如果传入其他值，会被先转成数值。比如，传入字符串的时候，字符串会被先转成 `NaN`，所以最后返回 `true`，这一点要特别引起注意。也就是说，**`isNaN` 为 `true` 的值，有可能不是 `NaN`，而是一个字符串**。

```js
isNaN("Hello"); // true
// 相当于
isNaN(Number("Hello")); // true
```

出于同样的原因，对于对象和数组，`isNaN`也返回`true`。

但是，对于空数组和只有一个数值成员的数组，`isNaN`返回`false`。

```js
isNaN([]); // false
isNaN([123]); // false
isNaN(["123"]); // false
```

上面代码之所以返回`false`，原因是这些数组能被`Number`函数转成数值

因此，使用`isNaN`之前，最好判断一下数据类型。

```js
function myIsNaN(value) {
  return typeof value === "number" && isNaN(value);
}
// OR
function myIsNaN(value) {
  return value !== value;
}
```
