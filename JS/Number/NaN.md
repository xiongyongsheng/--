# NaN

`NaN`是 `JavaScript` 的特殊值，表示“非数字”（Not a Number），主要出现在将字符串解析成数字出错的场合。

- 需要注意的是，`NaN`不是独立的数据类型，而是一个特殊数值，它的数据类型依然属于`Number`

- 数组的`indexOf`方法内部使用的是严格相等运算符，所以该方法对`NaN`不成立
- `NaN`与任何数（包括它自己）的运算，得到的都是`NaN`。

```js
0 / 0; // NaN
typeof NaN; // 'number'
[NaN].indexOf(NaN); // -1
```
