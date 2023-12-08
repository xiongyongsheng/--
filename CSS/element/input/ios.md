# ios 兼容性

#### 禁用 ios 搜索框自带的图标

```css
/* 禁用搜索框自带的图标 */
input[inputmode="search"]::-webkit-search-decoration,
input[inputmode="search"]::-webkit-search-cancel-button,
input[inputmode="search"]::-webkit-search-results-button,
input[inputmode="search"]::-webkit-search-results-decoration {
  display: none;
}
```

#### 禁用 ios 自带样式,使得自定义样式生效

```css
/* 禁用ios自带样式,使得自定义样式生效 */
input {
  -webkit-appearance: none;
}
```
