# db-webapp

> vue2.0 + vue-router + vue-resource  简单实现实现豆瓣webapp

目前实现了movie首页，路由切换，数据均来自[豆瓣API](https://developers.douban.com/wiki/?title=guide)

demo地址：
[https://liangxiaoxin.github.io/douban-webapp/](https://liangxiaoxin.github.io/douban-webapp/)


第三方插件：better-scorll.js 实现左右滑动
轮播图: mint-ui
动画：aminate.min.css
## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# run unit tests
npm run unit

# run all tests
npm test
```

------------------------------------------------这里是分割线-----------------------------------------------------
## 0801

上面是我直接clone下来的  然后在以上的基础上增加了一些

增加了电影详细页里面的演员介绍！

在moveMore.vue 里面增加了下拉加载更多 并不怎么流畅 (170804)

还有更多页面