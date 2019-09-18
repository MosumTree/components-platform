# Lazyload

懒加载组件

## 安装

### 使用 aio 进行安装(推荐)

```
$ aio i @cloud/lazyload -S
```

### 使用 npm 进行安装

```
$ npm config set @cloud:registry http://szg1.artifactory.inhuawei.com/artifactory/api/npm/npm-cbcbigate/
$ npm install @cloud/lazyload
```

### 使用 CDN 路径

其中{version}替换成对应的版本号即可。

```
https://res.hc-cdn.com/cnpm-lazyload/{version}/index.js
```

## 占位图片

图片懒加载时，经常会用到占位图，这里提供 2 个常用的

```
# 一个透明的点
http://res.hc-cdn.com/cnpm-lazyload/1.0.1/img/s.gif

# 华为logo
https://res.hc-cdn.com/cnpm-lazyload/1.0.1/img/b.png

```

## 用法

### 基本调用

```html
<div class="list">
    <img class="lazyload" data-src="http://www.placehold.it/375x200/eee/444/1" src="占位图片URL" />
    <img class="lazyload" data-src="http://www.placehold.it/375x200/eee/444/2" src="占位图片URL" />
    <img class="lazyload" data-src="http://www.placehold.it/375x200/eee/444/3" src="占位图片URL" />
    <div class="lazyload" data-src="http://www.placehold.it/375x200/eee/444/3"></div>
    ...
</div>
```

```javascript
import Lazyload from '@cloud/lazyload';

// 不传递container参数时，默认是document.body，即监听body内所有图片，建议配置container，尽可能减小计算量
new Lazyload(container);
```

### 说明

-   当`data-src`的标签是 img 时，默认是将`data-src`替换成`src`
-   当`data-src`的标签是非 img 时，如`div`,`span`，则是将`data-src`替换为 `style="background-image:url()"`

参数：

| Param                | Type                                          | Default         | Description                                                                                                                                  |
| -------------------- | --------------------------------------------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| [container]          | `String` or `HTMLElement` or `HTMLCollection` | `document.body` | 需要被加载的图片所在的容器                                                                                                                   |
| [config]             | `Object`                                      |                 |                                                                                                                                              |
| [config.rootMarginY] | `Number`                                      | 0               | 和 IntersectionObserver 的 rootMargin 含义一致，即图片距离视口多少 px 的时候开始加载，当不设置时默认为 0，并且在 onload 后会自动调整到 667px |
| [config.rootMarginX] | `Number`                                      | 0               | 和 IntersectionObserver 的 rootMargin 含义一致，即图片距离视口多少 px 的时候开始加载                                                         |
| [config.scroller]    | `String` or `HTMLElement`                     | `window`        | 需要监听的滚动容器，默认为 window，当不是 window 时，会在绑定对应容器的滚动的同时绑定 window 的滚动                                          |
| [config.processor]   | `function`                                    |                 | 在图片加载前对图片 src 进行处理                                                                                                              |

### 区域滚动

当滚动容器不是 window 时，需要设置`scroller`属性，这时 LazyLoad 会在监听 window 的`scroll`事件的同时，监听`scroller`的`scroll`事件

```html
<div class="scroller">
    <img class="lazyload" data-src="http://www.placehold.it/375x200/eee/444/1" src="占位图片URL" />
    <img class="lazyload" data-src="http://www.placehold.it/375x200/eee/444/2" src="占位图片URL" />
    <img class="lazyload" data-src="http://www.placehold.it/375x200/eee/444/3" src="占位图片URL" />
    ...
</div>
```

```javascript
import Lazyload from '@cloud/lazyload';

new Lazyload('.scroller', {
    // 滚动容器
    scroller: '.scroller',
});
```

### 图片链接处理

```javascript
import Lazyload from '@cloud/lazyload';
import CrossImage from '@cloud/crossImage';

new Lazyload('.scroller', {
    // processor可以用来在加载图片前对图片链接做处理，从而实现高清适配等需求，以对接mui/crossImage为例：
    processor: function(src, imgEl) {
        return Crossimage.getFitUrl(src, imgEl.width, imgEl.height);
    },
});
```

### 向实例添加监听对象

通过这种方式可以减少实例的创建和滚动等事件的绑定，减少懒加载对页面滚动流畅性的影响

```javascript
let lazyload = new Lazyload('#J_lazyloadA');

lazyload.addContainer('#J_lazyloadB');
```

参数：

| Param                | Type                                          | Default  | Description                                                                                         |
| -------------------- | --------------------------------------------- | -------- | --------------------------------------------------------------------------------------------------- |
| el                   | `String` or `HTMLElement` or `HTMLCollection` |          | 需要被监听的元素                                                                                    |
| callback             | `function`                                    |          | 回调函数                                                                                            |
| [config]             | `Object`                                      |          |                                                                                                     |
| [config.rootMarginY] | `Number`                                      |          | 和 IntersectionObserver 的 rootMargin 含义一致，即图片距离视口多少 px 的时候开始加载                |
| [config.rootMarginX] | `Number`                                      |          | 和 IntersectionObserver 的 rootMargin 含义一致，即图片距离视口多少 px 的时候开始加载                |
| [config.scroller]    | `String` or `HTMLElement`                     | `window` | 需要监听的滚动容器，默认为 window，当不是 window 时，会在绑定对应容器的滚动的同时绑定 window 的滚动 |

### 暂停/恢复懒加载

暂停/恢复懒加载的处理，例如在 tabview 的场景里，当某一屏被切走以后你需要暂停它的懒加载，切回来时再恢复

```javascript
let lazyload = new Lazyload('#J_lazyloadA');

// 暂停
lazyload.pause();
// 恢复
lazyload.resume();
```

### 刷新

用于当被监听容器内的 DOM 发生变化后，重新收需要被懒加载的图片

```javascript
let lazyload = new Lazyload('#J_lazyloadA');

lazyload.refresh();
```

### 原型方法 - 监听某个元素是否进入视口

```javascript
import Lazyload from '@cloud/lazyload'

// 当元素target进入视口后，执行回调
Lazyload.addListener(target, function(target){
    console.log('You see me!',target);
}, {
    // 同样支持rootMarginX\rootMarginY的配置
    ...
})
```

### 原型方法 - 判断某个元素是否在视口内

```javascript
import Lazyload from '@cloud/lazyload'

Lazyload.isInViewPort(target, {
    // 同样支持rootMarginX\rootMarginY的配置
    ...
})
```

参数：

| Param                | Type          | Default | Description                                                                          |
| -------------------- | ------------- | ------- | ------------------------------------------------------------------------------------ |
| el                   | `HTMLElement` |         | 需要被判断的元素                                                                     |
| [config]             | `Object`      |         |                                                                                      |
| [config.rootMarginY] | `Number`      | `0`     | 和 IntersectionObserver 的 rootMargin 含义一致，即图片距离视口多少 px 的时候开始加载 |
| [config.rootMarginX] | `Number`      | `0`     | 和 IntersectionObserver 的 rootMargin 含义一致，即图片距离视口多少 px 的时候开始加载 |

更多 API 请查看文档 [http://ipages.huawei.com/cnpm/lazyload](http://ipages.huawei.com/cnpm/lazyload/globals.html)

## 组件维护者

@华宇果 (huayuguo@huawei.com)