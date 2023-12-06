---
title: git fork 同步
date: 2023-12-06 10:18:47
tags: git
---

### 场景
`自己工程为my，fork的主项目为base`
<!-- more -->


### 命令

* git remote add base https://gitee.com/chenshiyun/springboot-assembly-mybatis

* git fetch base

* git checkout sit
* git merge base/sit
