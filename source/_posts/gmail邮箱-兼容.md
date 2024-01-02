---
title: gmail邮箱-兼容
date: 2024-01-02 14:07:15
tags: 其它 兼容
---
### Gmail邮箱兼容性记录

[Gmail邮件关于支持HTML样式问题](https://www.jianshu.com/p/9daa461fe782)

<!-- more -->
补充：
* gmail不支持media query；
* 对于文本需添加font-size字体属性，否则gmail重置font-size；
* 安卓移动端--默认a标签`text-decoration`为none，若a标签需下划线需加上`text-decoration:underline;`