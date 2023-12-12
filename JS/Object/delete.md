# Delete

- 删除一个**不存在的属性**，`delete`不报错，而且返回`true`。

```js
var obj = {};
delete obj.p; // true
```

- 只有一种情况，`delete`命令会返回`false`，那就是该属性存在，且不得删除。

```js
var obj = Object.defineProperty({}, "p", {
  value: 123,
  configurable: false,
});

obj.p; // 123
delete obj.p; // false
```

- `delete`命令只能删除**对象本身**的属性，无法删除继承的属性

```js
var obj = {};
delete obj.toString; // true
obj.toString; // function toString() { [native code] }
```

> 这个例子还说明，即使 `delete` 返回 `true`，该属性依然可能读取到值。
