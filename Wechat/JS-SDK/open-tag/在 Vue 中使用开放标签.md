#在 Vue 中使用微信 JS-SDK 开放标签

- 在 **vue3** 中使用时:

```html
<wx-open-launch-weapp appid="<appid>" path="<pagePath>?<key>=<value>">
  <component :is="'script'" type="text/wxtag-template">
    <!-- content -->
  </component>
</wx-open-launch-weapp>
```
