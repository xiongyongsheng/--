## 类似数组的对象

如果一个对象的**所有键名**都是正整数或零，**并且有`length`属性**，那么这个对象就很像数组，语法上称为“类似数组的对象”（array-like object）。

```javascript
var obj = {
  0: "a",
  1: "b",
  2: "c",
  length: 3,
};

obj[0]; // 'a'
obj[1]; // 'b'
obj.length; // 3
obj.push("d"); // TypeError: obj.push is not a function
```

上面代码中，对象`obj`就是一个类似数组的对象。但是，“类似数组的对象”并不是数组，因为它们不具备数组特有的方法。对象`obj`没有数组的`push`方法，使用该方法就会报错。

“类似数组的对象”的根本特征，就是具有`length`属性。只要有`length`属性，就可以认为这个对象类似于数组。但是有一个问题，这种`length`属性不是动态值，不会随着成员的变化而变化。

```javascript
var obj = {
  length: 0,
};
obj[3] = "d";
obj.length; // 0
```

上面代码为对象`obj`添加了一个数字键，但是`length`属性没变。这就说明了`obj`不是数组。

典型的“类似数组的对象”是函数的`arguments`对象，以及大多数 DOM 元素集，还有字符串。

```javascript
// arguments对象
function args() {
  return arguments;
}
var arrayLike = args("a", "b");

arrayLike[0]; // 'a'
arrayLike.length; // 2
arrayLike instanceof Array; // false

// DOM元素集
var elts = document.getElementsByTagName("h3");
elts.length; // 3
elts instanceof Array; // false

// 字符串
"abc"[1]; // 'b'
"abc".length; // 3
"abc" instanceof Array; // false
```

上面代码包含三个例子，它们都不是数组（`instanceof`运算符返回`false`），但是看上去都非常像数组。

数组的`slice`方法可以将“类似数组的对象”变成真正的数组。

```javascript
var arr = Array.prototype.slice.call(arrayLike);
```

除了转为真正的数组，“类似数组的对象”还有一个办法可以使用数组的方法，就是通过`call()`把数组的方法放到对象上面。

```javascript
function print(value, index) {
  console.log(index + " : " + value);
  0;
}

Array.prototype.forEach.call(arrayLike, print);
```

上面代码中，`arrayLike`代表一个类似数组的对象，本来是不可以使用数组的`forEach()`方法的，但是通过`call()`，可以把`forEach()`嫁接到`arrayLike`上面调用。

下面的例子就是通过这种方法，在`arguments`对象上面调用`forEach`方法。

```javascript
// forEach 方法
function logArgs() {
  Array.prototype.forEach.call(arguments, function (elem, i) {
    console.log(i + ". " + elem);
  });
}

// 等同于 for 循环
function logArgs() {
  for (var i = 0; i < arguments.length; i++) {
    console.log(i + ". " + arguments[i]);
  }
}
```

**字符串也是类似数组的对象**，所以也可以用`Array.prototype.forEach.call`遍历。

```javascript
Array.prototype.forEach.call("abc", function (chr) {
  console.log(chr);
});
// a
// b
// c
```

注意，这种方法比直接使用数组原生的`forEach`要**慢**，所以最好还是先将“类似数组的对象”转为真正的数组，然后再直接调用数组的`forEach`方法。

```javascript
var arr = Array.prototype.slice.call("abc");
arr.forEach(function (chr) {
  console.log(chr);
});
// a
// b
// c
```
