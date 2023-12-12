# name

- 函数的`name`属性返回函数的名字.

```js
function f1() {}
f1.name; // "f1"
```

- 如果是通过变量赋值定义的函数，那么`name`属性返回变量名。

```js
var f2 = function () {};
f2.name; // "f2"
```

- 如果变量的值是一个具名函数，那么 `name` 属性返回 `function` 关键字之后的那个函数名。

```js
var f3 = function myName() {};
f3.name; // 'myName'
```
