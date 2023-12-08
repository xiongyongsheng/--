# praseFloat

`parseFloat`方法用于将一个字符串转为浮点数。

- 如果字符串符合科学计数法，则会进行相应的转换。

```js
parseFloat("314e-2"); // 3.14
parseFloat("0.0314E+2"); // 3.14
```

- `parseFloat`方法会自动过滤字符串前导的空格。

```js
parseFloat("\t\v\r12.34\n "); // 12.34
```

- 如果参数不是字符串，则会先转为字符串再转换。

```js
parseFloat([1.23]); // 1.23
// 等同于
parseFloat(String([1.23])); // 1.23
```

- 如果字符串的第一个字符不能转化为浮点数，则返回 NaN。

```js
parseFloat([]); // NaN
parseFloat("FF2"); // NaN
parseFloat(""); // NaN
```

上面代码中，尤其值得注意，`parseFloat` 会将空字符串转为 `NaN`。

这些特点使得 `parseFloat` 的转换结果不同于 `Number` 函数。

```js
parseFloat(true); // NaN
Number(true); // 1

parseFloat(null); // NaN
Number(null); // 0

parseFloat(""); // NaN
Number(""); // 0

parseFloat("123.45#"); // 123.45
Number("123.45#"); // NaN
```
