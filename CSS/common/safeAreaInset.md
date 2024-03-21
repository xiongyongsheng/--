# 移动设备适配底部安全距离

`safe-area-inset-bottom` 是一个 CSS 变量，用于在移动设备上处理屏幕底部的安全区域。在 iPhone X 及更高版本的设备上，由于底部的 Home Indicator 和底部滑动手势区域，需要给用户留出一定的安全区域，以免内容被遮挡或者操作受到影响。

通过使用 `safe-area-inset-bottom` 变量，可以在 CSS 中动态地应用底部安全区域的大小，确保页面内容不会被底部的操作区域遮挡。例如，可以将这个变量应用到固定在页面底部的元素的底部内边距中，以便在不同设备上正确显示。

```css
.element {
  padding-bottom: constant(
    safe-area-inset-bottom
  ); /* 针对不支持环境的备用方案 */
  padding-bottom: env(safe-area-inset-bottom); /* 标准语法 */
}
```

需要注意的是，`safe-area-inset-bottom` 变量在不同浏览器和设备上的支持情况可能会有所不同，因此在使用时需要进行兼容性测试。
