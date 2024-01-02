---
title: lerna常用命令
date: 2024-01-02 13:09:18
tags: 工具
---

### lerna
``lerna ls ``
``lerna clean ``
#### 添加依赖
``lerna add lodash``   *给所有 package 安装依赖*
``lerna add element-ui@2.15.8 --scope=@packagename``   *给指定package安装依赖*
<!-- more -->

#### package软链
``lerna link``

#### 更新依赖
``lerna bootstrap``  *所有子包更新依赖*

#### 打包构建
``lerna run build``  *运行所有包的build命令*
``lerna run --scope @packagename build`` *运行指定包依赖*
### 发布
``lerna publish``

