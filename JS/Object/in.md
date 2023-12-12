# In

- `in`运算符的一个问题是，它**不能识别**哪些属性是对象自身的，哪些属性是继承的.

```js
var obj = {};
if ("toString" in obj) {
  console.log(obj.hasOwnProperty("toString")); // false
}
```
