# For...in

- 它遍历的是对象所有可遍历（`enumerable`）的属性，**会跳过**不可遍历的属性。

```js
var obj = {};

// toString 属性是存在的
obj.toString; // toString() { [native code] }

for (var p in obj) {
  console.log(p);
} // 没有任何输出
```

- 它不仅遍历对象自身的属性，**还遍历继承的属性**。

```js
var person = { name: "老张" };

for (var key in person) {
  // 只想遍历对象自身的属性
  if (person.hasOwnProperty(key)) {
    console.log(key);
  }
}
// name
```
