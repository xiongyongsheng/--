# structuredClone()

全局的 `structuredClone()` 方法使用结构化克隆算法将给定的值进行**深拷贝**。

该方法还支持把原始值中的`可转移对象`转移到新对象，而不是把属性引用拷贝过去。 `可转移对象`与原始对象分离并附加到新对象;它们不可以在原始对象中访问被访问到。

```js
structuredClone(value);
structuredClone(value, { transfer });
```

### value 参数

这个函数可以用来进行深拷贝 `JavaScript` 变量。 也**支持循环引用**

```js
const original = { name: "MDN" };
original.itself = original;

const clone = structuredClone(original);

console.assert(clone !== original); \\ true
console.assert(clone.name === "MDN");\\ true
console.assert(clone.itself === clone);\\ true
```

### transfer 参数

使用可选参数 `transfer` 里的值，可以使可转移对象（仅）**被传递**，**不被**克隆。 传输导致原始对象（里的属性）**无法**继续使用。

```js
var uInt8Array = new Uint8Array(1024 * 1024 * 16); // 16MB
for (var i = 0; i < uInt8Array.length; ++i) {
  uInt8Array[i] = i;
}

const transferred = structuredClone(uInt8Array, {
  transfer: [uInt8Array.buffer],
});
console.log(uInt8Array.byteLength); // 0
```

你可以克隆任意数量的对象，并传输对象的任意子集。 例如 以下代码会把 `arrayBuffer1` 作为值传输 但**不是** `arrayBuffer2`。

```js
const transferred = structuredClone(
  { x: { y: { z: arrayBuffer1, w: arrayBuffer2 } } },
  { transfer: [arrayBuffer1] }
);
```

### 与 JSON.parse(JSON.stringify(Object)) 比较

`structuredClone()` 方法与 `JSON.parse(JSON.stringify(Object))` 方法相比，有以下优势：

- 它支持循环引用。
- 它支持 `ArrayBuffer` 和 `SharedArrayBuffer`。
- 它支持 `DataView`。
- 它支持 `Map` 和 `Set`。
- 它支持 `WeakMap` 和 `WeakSet`。
- 它支持 `TypedArray`。
- 它支持 `Blob`。
- 它支持 `File`。
- 它支持 `ImageBitmap`。
- 它支持 `ImageData`。
- 它支持 `Regex`。

### 与\_.cloneDeep 比较

`structuredClone()` 方法与 `_.cloneDeep(Object)` 方法相比，有以下优势：

- 浏览器内置支持.
- 增加了项目的大小.(_约 25kb_)

### 限制

[支持的类型(MDN)](https://developer.mozilla.org/zh-CN/docs/Web/API/Web_Workers_API/Structured_clone_algorithm#%E6%94%AF%E6%8C%81%E7%9A%84%E7%B1%BB%E5%9E%8B)
