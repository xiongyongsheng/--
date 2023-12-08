# Intl (i18n)

**Intl** 是 **JavaScript** 中用于国际化（_Internationalization_，简称 _i18n_）的内置对象。它提供了一系列用于处理日期、时间、数字格式化以及排序比较的功能，以便在不同的语言和地区环境下正确地显示和处理文本和数据。

下面是 Intl 对象提供的一些常见功能：

- 格式化日期和时间：`Intl.DateTimeFormat` 对象可以用来格式化日期和时间，根据不同的语言和地区习惯显示日期和时间格式。

- 格式化数字：`Intl.NumberFormat` 对象可以用来格式化数字，根据不同的语言和地区规范显示数字格式、货币符号和小数点等。

- 排序比较：`Intl.Collator` 对象可以用来进行字符串的排序比较，根据不同的语言和地区规范进行正确的排序。

这些功能使得开发者可以编写能够适应不同语言和地区的应用程序，同时确保文本和数据以用户所在地区的习惯和规范进行正确的显示和处理。

例如，以下是使用 `Intl.NumberFormat` 对象格式化数字的示例：

```js
let number = 123456.789;

let formatter = new Intl.NumberFormat("en-US", {
  style: "currency",
  currency: "USD",
});

console.log(formatter.format(number));
```

在上面的示例中，我们创建了一个 `Intl.NumberFormat` 对象，用于将数字格式化为美元货币格式。这样可以确保数字在美国地区的货币显示规范下进行正确的格式化。

总之，Intl 对象为 JavaScript 提供了强大的国际化功能，使得开发者能够编写能够适应不同语言和地区的应用程序。
