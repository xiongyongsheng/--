#使用 CSS Filter 属性 实现 skeleton (骨架屏) 加载效果

    市面上绝大多数骨架屏解决方案都是维护两套代码(业务代码和骨架屏代码分开写)
    本方案诣在只用一套代码,减少后期维护工作量.

##使用方法

1. 全局引入下方 css 代码(或者在需要的页面引入).
2. 准备好`mock data`,在真实的数据返回之前先填充页面.
3. 在需要做`骨架加载`的标签上加上`skeleton`属性.
4. (可选)在加上了`skeleton`的标签的祖先标签上加伤`skeleton-switch`属性.
5. 通过控制`skeleton`属性或者其祖先标签的`skeleton-switch`属性的值为`true`来控制是否显示`骨架加载`效果.

####CSS 代码

```css
*[skeleton-switch="true"] *[skeleton=""],
*[skeleton="true"] {
  --filter: contrast(0%) brightness(1.85);
  /* 必须有背景颜色 filter: contrast(0%) 才能生效 */
  background-color: #fff !important;
  filter: var(--filter);
  animation: skeleton-animation infinite ease-in-out 1.2s;
  pointer-events: none;
}
*[skeleton-switch="true"] *[skeleton=""] *,
*[skeleton="true"] * {
  pointer-events: none;
}
*[skeleton-switch="true"] {
  position: relative;
}
*[skeleton-switch="true"]::before {
  display: none !important;
}
*[skeleton-switch="true"]::after {
  all: unset !important;
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0);
  z-index: 9999;
}
@keyframes skeleton-animation {
  0% {
    filter: var(--filter);
  }
  50% {
    filter: contrast(0%) brightness(1.7);
  }
  100% {
    filter: var(--filter);
  }
}
```

####优缺点

- **缺点**:

  1. CSS 中的 `filter` 有一定的浏览器兼容性问题 (主流现代浏览器都支持).
  2. 需要先准备一份 `mock data` 来填充页面.
  3. 可能会影响到页面的布局. (比如祖先元素的伪元素`::before`,`::after`)
  4. 加载的动画效果比较一般,不能做额外的动效(因为`filter: contrast(0%)`会把所有的颜色都变成灰色).

- **优点**:
  1. 减少后期维护的工作量,共用骨架屏代码和真实页面的代码,不需要单独维护一套骨架屏代码.(页面发生改动时,几乎不需要动骨架屏代码.)
  2. 使用简单,不需要复杂的配置.
  3. 代码量小,不需要额外的优化.

####例子

```html
<section class="c-card" id="c-outlets-card" :skeleton-switch="isShowSkeleton">
  <div class="c-card-head">
    <h5>适老网点信息</h5>
  </div>
  <article class="c-card-body">
    <van-pull-refresh v-model="refreshing" @refresh="onRefresh">
      <van-list
        v-model:loading="loading"
        v-model:error="error"
        :finished="finished"
        @load="onLoad"
      >
        <section class="c-cell-bank" v-for="item in list" :key="item.id">
          <div>
            <h6 skeleton>{{ item.name }}</h6>
            <p skeleton>{{ item.address }}</p>
            <a skeleton :href="`tel:${item.tel}`">
              <img src="@/assets/适老网点/编组备份6@3x.png" alt="tel" />{{
              item.tel }}
            </a>
          </div>
          <div @click="handleNavigator(item)">
            <img
              skeleton
              src="@/assets/适老网点/编组2@3x.png"
              alt="navigation"
            />
            <span skeleton>导航</span>
          </div>
        </section>
        <van-empty
          image="search"
          v-if="!list.length && finished"
          description="暂无记录"
        />
        <template #error>
          <van-empty
            image="network"
            :description="errorDescription || '网络错误'"
          />
        </template>
      </van-list>
    </van-pull-refresh>
  </article>
</section>
```
