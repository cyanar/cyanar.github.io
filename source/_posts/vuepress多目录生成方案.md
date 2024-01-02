---
title: vuepress多目录生成方案
date: 2024-01-02 14:33:48
tags: vuepress
---

### 背景
vuepress 版本^1.4.1
需要自定义首页，搭建文档库集合，每个入口对应不同的sidebar
<!-- more -->
### 首页改造
在.vuepress目录新建components文件夹，新建Home.vue
```html
<template>
  <div class="api-doc">
    <a href="/doc/sidebar1/" class="card">
      <img src="111">
      <div class="api-desc">
        <a  href="/doc/sidebar1/">doc1</a>
        <p class="des">我是doc1的描述</p>
      </div>
    </a>
    <a href="/doc/sidebar2/" class="card">
      <img src="222">
      <div class="api-desc">
        <a href="/doc/sidebar2/">doc2</a>
        <p class="des">我是doc2的描述</p>
      </div>
    </a>
    <a href="/doc/sidebar3/" class="card">
      <img src="333">
      <div class="api-desc">
        <a href="/doc/sidebar3/">doc3</a>
        <p class="des">我是doc3的描述</p>
      </div>
    </a>
  </div>
</template>

<script>
export default {

}
</script>

<style>
.api-doc {
  display: flex;
  flex-wrap: wrap;
  height: 60%;
  margin-bottom: 10%;
}
.card {
  width: 29.6%;
  height: 60px;
  margin: 10px 0;
  margin-right: 2%;
  padding: 10px;
  display: flex;
  justify-content: space-around;
  align-items: center;
  border-radius: 4px;
  cursor: pointer;
  box-shadow: 0px 0px 2px rgba(0,0,0,0.16),0px 1px 3px 1px rgba(0,0,0,0.08);
}
.card:nth-child(3n) {
  margin-right: 0;
}
.card:hover {
  box-shadow: 0px 0px 2px rgba(0,0,0,0.16),0px 1px 3px 1px rgba(0,0,0,0.15);
}
.card img {
  width: 40px;
  height: 40px;
  border-radius: 50%;
}
.card .api-desc  {
  width: 80%;
}
.api-desc .des {
  font-size: 12px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  margin: 0;
  color: rgb(147,147,147);
}
</style>
```
在.vuepress目录新建clientAppEnhance.js，注册VUE组件
```js
import { defineClientAppEnhance } from '@vuepress/client'
import Home from './components/Home.vue'

export default defineClientAppEnhance(({ app, router, siteData }) => {
  app.component('Home', Home)
})
```

然后docs根目录`README.md`改写为：
```markdown
---
home: true
footer: MIT Licensed | Copyright © 2023
---
<ClientOnly>
<Home/>
</ClientOnly>
```
### sidebar改造
在.vuepress目录新建sidebars文件夹，包含不同路径的sidebar文件：
```
|-- .vuepress       
  |-- sidebars
    |-- doc1.js 
    |-- doc2.js 
```
doc1.js
```js
module.exports = [
  ['/doc1/', 'DOC1文档'],
  {
    title: '功能介绍',
    collapsable: true,
    children: [
        ['/doc1/test.md', "测试"],
        ['/doc1/test2.md', "测试2"]
    ]
  }
];
```
在.vuepress目录config.js添加配置：
```js
const doc1Sidebar = require('./sidebars/doc1');
const doc2Sidebar = require('./sidebars/doc2');

module.exports = {
  themeConfig: {
      sidebar: {
      '/doc1/': doc1Sidebar,
      '/doc2/': doc2Sidebar,
      },
  },
  configureWebpack: config => {
    config.output.publicPath = '/doc/';
  }
}
```
### nginx配置
部署上去，因为nginx打包为多页面，点击可能会报错`Failed to execute 'appendChild' on 'Node`，需要配置下
```
location /doc1 {
  root /usr/share/nginx/html;
  try_files $uri $uri /doc1/index.html;
}

location /doc2 {
  root /usr/share/nginx/html;
  try_files $uri $uri /doc2/index.html;
}

```

### 参考
[vuePress2.x 多页面](https://www.cnblogs.com/dingshaohua/p/15386262.html)
