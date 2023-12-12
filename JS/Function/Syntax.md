# Function

### 创建函数的三种方式

1. 函数的声明.

```js
function print() {}
```

2. 函数表达式.

```js
var print = function (s) {};
```

> 采用函数表达式声明函数时，`function` 命令后面不带有函数名。如果加上函数名，该函数名只在函数体内部有效，在函数体外部无效。

```js
var print = function x() {};

x;
// ReferenceError: x is not defined

print();
// function
```

3. Function 构造函数

```js
var add = new Function("x", "y", "return x + y");

// 等同于
function add(x, y) {
  return x + y;
}
```

> 这种声明函数的方式非常不直观，几乎无人使用。

`JavaScript` 语言将函数看作一种值，与其它值（数值、字符串、布尔值等等）地位相同。凡是可以使用值的地方，就能使用函数。比如，可以把函数赋值给变量和对象的属性，也可以当作参数传入其他函数，或者作为函数的结果返回。函数只是一个可以执行的值，此外并无特殊之处。

### 函数提升

- `JavaScript` 引擎将函数名视同变量名，所以采用`function`命令声明函数时，整个函数会像变量声明一样，被提升到代码头部。

- **如果采用赋值语句定义函数，`JavaScript` 就会报错**。

```js
f();
var f = function () {};
// TypeError: undefined is not a function
```

- 如果像下面例子那样，采用`function`命令和`var`赋值语句声明同一个函数，**由于存在函数提升，最后会采用`var`赋值语句的定义**。

```js
var f = function () {};

function f() {}

f(); // 1
```

## function scope

三种作用域

- 全局作用域,变量在整个程序中一直存在，所有地方都可以读取
- 函数作用域，变量只在函数内部存在
- `ES6` 又新增了块级作用域

> 注意，对于`var`命令来说，**局部变量只能在函数内部声明**，在其他区块中声明，一律都是全局变量。

```js
if (true) {
  var x = 5;
}
// 5
```

与全局作用域一样，函数作用域内部也会产生“变量提升”现象。`var` 命令声明的变量，不管在什么位置，变量声明都会被提升到函数体的头部。

```js
function foo(x) {
  if (x > 100) {
    var tmp = x - 100;
  }
}

// 等同于
function foo(x) {
  var tmp;
  if (x > 100) {
    tmp = x - 100;
  }
}
```

函数本身也是一个值，也有自己的作用域。它的作用域与变量一样，**就是其声明时所在的作用域**，**与其运行时所在的作用域无关**。

```js
var a = 1;
var x = function () {};

function f() {
  var a = 2;
  x();
}

f(); // 1

// 闭包
function foo() {
  var x = 1;
  function bar() {}
  return bar;
}

var x = 2;
var f = foo();
f(); // 1
```

## 传递方式

- 函数参数如果是原始类型的值（数值、字符串、布尔值），传递方式是传值传递（passes by value）。这意味着，在函数体内修改参数值，不会影响到函数外部。

```js
var p = 2;

function f(p) {
  p = 3;
}
f(p);

p; // 2
```

- 如果函数参数是复合类型的值（数组、对象、其他函数），传递方式是传址传递（pass by reference）。也就是说，传入函数的原始值的地址，因此在函数内部修改参数，将会影响到原始值。

```js
var obj = { p: 1 };

function f(o) {
  o.p = 2;
}
f(obj);

obj.p; // 2
```

**注意，如果函数内部修改的，不是参数对象的某个属性，而是替换掉整个参数，这时不会影响到原始值。**

```js
var obj = [1, 2, 3];

function f(o) {
  o = [2, 3, 4];
}
f(obj);

obj; // [1, 2, 3]
```

上面代码中，在函数 `f()`内部，参数对象 `obj` 被整个替换成另一个值。这时不会影响到原始值。这是因为，形式参数（`o`）的值实际是参数 `obj` 的地址，重新对 `o` 赋值导致 `o` 指向另一个地址，保存在原地址上的值当然不受影响。

### 同名参数

如果有同名的参数，则取最后出现的那个值。

```javascript
function f(a, a) {
  console.log(a);
}

f(1, 2); // 2
```

上面代码中，函数`f()`有两个参数，且参数名都是`a`。取值的时候，以后面的`a`为准，即使后面的`a`没有值或被省略，也是以其为准。

```javascript
function f(a, a) {
  console.log(a);
}

f(1); // undefined
```

调用函数`f()`的时候，没有提供第二个参数，`a`的取值就变成了`undefined`。这时，如果要获得第一个`a`的值，可以使用`arguments`对象。

```javascript
function f(a, a) {
  console.log(arguments[0]);
}

f(1); // 1
```

### arguments 对象

**（1）定义**

正常模式下，`arguments`对象可以在运行时修改。

```javascript
var f = function (a, b) {
  arguments[0] = 3;
  arguments[1] = 2;
  return a + b;
};

f(1, 1); // 5
```

上面代码中，函数`f()`调用时传入的参数，在函数内部被修改成`3`和`2`。

严格模式下，`arguments`对象与函数参数不具有联动关系。也就是说，修改`arguments`对象不会影响到实际的函数参数。

```javascript
var f = function (a, b) {
  "use strict"; // 开启严格模式
  arguments[0] = 3;
  arguments[1] = 2;
  return a + b;
};

f(1, 1); // 2
```

上面代码中，函数体内是严格模式，这时修改`arguments`对象，不会影响到真实参数`a`和`b`。

通过`arguments`对象的`length`属性，可以判断函数调用时到底带几个参数。

```javascript
function f() {
  return arguments.length;
}

f(1, 2, 3); // 3
f(1); // 1
f(); // 0
```

**（2）与数组的关系**

需要注意的是，虽然`arguments`很像数组，但它是一个对象。数组专有的方法（比如`slice`和`forEach`），不能在`arguments`对象上直接使用。

如果要让`arguments`对象使用数组方法，真正的解决方法是将`arguments`转为真正的数组。下面是两种常用的转换方法：`slice`方法和逐一填入新数组。

```javascript
var args = Array.prototype.slice.call(arguments);

// 或者
var args = [];
for (var i = 0; i < arguments.length; i++) {
  args.push(arguments[i]);
}
```

**（3）callee 属性**

`arguments`对象带有一个`callee`属性，返回它所对应的原函数。

```javascript
var f = function () {
  console.log(arguments.callee === f);
};

f(); // true
```

可以通过`arguments.callee`，达到调用函数自身的目的。这个属性在严格模式里面是禁用的，因此不建议使用。
