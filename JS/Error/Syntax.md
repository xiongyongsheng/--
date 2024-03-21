# 错误处理机制

## Error 实例对象

JavaScript 解析或运行时，一旦发生错误，引擎就会抛出一个错误对象。JavaScript 原生提供`Error`构造函数，所有抛出的错误都是这个构造函数的实例。

```javascript
var err = new Error("出错了");
err.message; // "出错了"
```

上面代码中，我们调用`Error()`构造函数，生成一个实例对象`err`。`Error()`构造函数接受一个参数，表示错误提示，可以从实例的`message`属性读到这个参数。抛出`Error`实例对象以后，整个程序就中断在发生错误的地方，不再往下执行。

JavaScript 语言标准只提到，`Error`实例对象必须有`message`属性，表示出错时的提示信息，没有提到其他属性。大多数 JavaScript 引擎，对`Error`实例还提供`name`和`stack`属性，分别表示错误的名称和错误的堆栈，但它们是非标准的，不是每种实现都有。

- **message**：错误提示信息
- **name**：错误名称（非标准属性）
- **stack**：错误的堆栈（非标准属性）

使用`name`和`message`这两个属性，可以对发生什么错误有一个大概的了解。

```javascript
if (error.name) {
  console.log(error.name + ": " + error.message);
}
```

`stack`属性用来查看错误发生时的堆栈。

```javascript
function throwit() {
  throw new Error("");
}

function catchit() {
  try {
    throwit();
  } catch (e) {
    console.log(e.stack); // print stack trace
  }
}

catchit();
// Error
//    at throwit (~/examples/throwcatch.js:9:11)
//    at catchit (~/examples/throwcatch.js:3:9)
//    at repl:1:5
```

上面代码中，错误堆栈的最内层是`throwit`函数，然后是`catchit`函数，最后是函数的运行环境。

## 原生错误类型

`Error`实例对象是最一般的错误类型，在它的基础上，JavaScript 还定义了其他 6 种错误对象。也就是说，存在`Error`的 6 个派生对象。

### SyntaxError 对象

`SyntaxError`对象是解析代码时发生的语法错误。

```javascript
// 变量名错误
var 1a;
// Uncaught SyntaxError: Invalid or unexpected token

// 缺少括号
console.log 'hello');
// Uncaught SyntaxError: Unexpected string
```

上面代码的错误，都是在语法解析阶段就可以发现，所以会抛出`SyntaxError`。第一个错误提示是“token 非法”，第二个错误提示是“字符串不符合要求”。

### ReferenceError 对象

`ReferenceError`对象是引用一个不存在的变量时发生的错误。

```javascript
// 使用一个不存在的变量
unknownVariable;
// Uncaught ReferenceError: unknownVariable is not defined
```

另一种触发场景是，将一个值分配给无法分配的对象，比如对函数的运行结果赋值。

```javascript
// 等号左侧不是变量
console.log() = 1
// Uncaught ReferenceError: Invalid left-hand side in assignment
```

上面代码对函数`console.log`的运行结果赋值，结果引发了`ReferenceError`错误。

### RangeError 对象

`RangeError`对象是一个值超出有效范围时发生的错误。主要有几种情况，一是数组长度为负数，二是`Number`对象的方法参数超出范围，以及函数堆栈超过最大值。

```javascript
// 数组长度不得为负数
new Array(-1);
// Uncaught RangeError: Invalid array length
```

### TypeError 对象

`TypeError`对象是变量或参数不是预期类型时发生的错误。比如，对字符串、布尔值、数值等原始类型的值使用`new`命令，就会抛出这种错误，因为`new`命令的参数应该是一个构造函数。

```javascript
new 123();
// Uncaught TypeError: 123 is not a constructor

var obj = {};
obj.unknownMethod();
// Uncaught TypeError: obj.unknownMethod is not a function
```

上面代码的第二种情况，调用对象不存在的方法，也会抛出`TypeError`错误，因为`obj.unknownMethod`的值是`undefined`，而不是一个函数。

### URIError 对象

`URIError`对象是 URI 相关函数的参数不正确时抛出的错误，主要涉及`encodeURI()`、`decodeURI()`、`encodeURIComponent()`、`decodeURIComponent()`、`escape()`和`unescape()`这六个函数。

```javascript
decodeURI("%2");
// URIError: URI malformed
```

### EvalError 对象

`eval`函数没有被正确执行时，会抛出`EvalError`错误。该错误类型已经不再使用了，只是为了保证与以前代码兼容，才继续保留。

### 总结

以上这 6 种派生错误，连同原始的`Error`对象，都是构造函数。开发者可以使用它们，手动生成错误对象的实例。这些构造函数都接受一个参数，代表错误提示信息（message）。

```javascript
var err1 = new Error("出错了！");
var err2 = new RangeError("出错了，变量超出有效范围！");
var err3 = new TypeError("出错了，变量类型无效！");

err1.message; // "出错了！"
err2.message; // "出错了，变量超出有效范围！"
err3.message; // "出错了，变量类型无效！"
```
