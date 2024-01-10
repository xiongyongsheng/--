## in

检查某个键名是否存在的运算符`in`，适用于对象，也适用于数组。

```javascript
var arr = ["a", "b", "c"];
2 in arr; // true
"2" in arr; // true
4 in arr; // false
```

上面代码表明，数组存在键名为`2`的键。由于键名都是字符串，所以**数值`2`会自动转成字符串**。

**注意，如果数组的某个位置是空位，`in`运算符返回**`false`。

```javascript
var arr = [];
arr[100] = "a";

100 in arr; // true
1 in arr; // false
```

上面代码中，数组`arr`只有一个成员`arr[100]`，其他位置的键名都会返回`false`。
