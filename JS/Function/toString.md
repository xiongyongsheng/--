# toString

函数的`toString()`方法返回一个字符串，内容是函数的源码。

- 对于那些原生的函数，`toString()`方法返回 `function (){[native code]}`。

```js
Math.sqrt.toString();
// "function sqrt() { [native code] }"
```

- 非原生函数返回的源码，**包含换行符**在内。

```js
function f() {
  a();
  b();
  c();
}

f.toString();
// function f() {
//  a();
//  b();
//  c();
// }
```

利用这一点，可以变相实现多行字符串。

```js
var multiline = function (fn) {
  var arr = fn.toString().split("\n");
  return arr.slice(1, arr.length - 1).join("\n");
};

function f() {
  /*
  这是一个
  多行注释
*/
}

multiline(f);
// " 这是一个
//   多行注释"
```

上面示例中，函数`f`内部有一个多行注释，`toString()`方法拿到`f`的源码后，去掉首尾两行，就得到了一个多行字符串。
