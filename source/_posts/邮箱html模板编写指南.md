---
title: 邮箱html模板编写指南
date: 2024-01-02 14:01:03
tags: 其它 兼容
---

#### 兼容性

主要兼容海外主流邮箱设备，已确认和已测试过的：
* Gmail -- web端、mac应用、移动端（安卓&IOS）
* Outlook -- web端、mac应用、移动端（安卓&IOS）、windows客户端（16/19/21/23版本）
* 苹果icoud -- 移动端IOS、mac内置邮箱应用
* Exchange（邮件服务器）
* 雅虎 -- web端

<!-- more -->

#### 全局规则
1. `doctype,body`和`meta`之类的标签一般不用写，因为在很多邮箱系统里它会被过滤；
2. <font color=red>禁止外联CSS/JS/iframe</font>，所有样式用style写内联的CSS；
3. 少用图片，邮箱不会过滤你的img标签，但是系统往往会默认不载入陌生来信的图片，如果用了很多图片的邮件，在图片没有载入的情况下，会看不清内容，没耐心的用户直接就删除了。图片上务必加上alt；
4. 全部使用<font color=red>table布局</font>，避免使用float、position，flex布局，outlook不支持。推荐标签
<font color=red>table / tr / td / span / img / a</font>
，尽量避免使用div、p及其他标签；

5. 不允许在`<tr>`元素上定义CSS样式，样式尽量定义在`<td>`元素上（Gmail等邮件客户端会过滤`<tr>`上的属性）；
6. 充分利用标签的私有属性来布局,如<font color=red>width, height, bgcolor, background, align, valign</font>等：
```
<img width="10" height="10" src="*.png" />
```
7. CSS属性不要简写，尤其padding属性--主要为了兼容outlook邮箱，如：
```
 <td style="padding-left:16px;padding-top:24px;padding-right:16px;padding-bottom:0;">
```
8. 关于字体--有时设计师会让你使用特定字体，而邮件里面一般使用的是系统支持的字体，如果不支持，将会变成默认字体；

9. [Outlook兼容](https://yunxii.cn/)


10. [Gmail兼容](https://yunxii.cn/)
#### 参考
[邮件样式支持查询](https://www.campaignmonitor.com/css/)

[不同邮件服务商读取 HTML 邮件已知问题一览表](http://app1.studiocloud.com/support/index.php?/article/AA-00861/0/Issues-with-HTML-Emails-in-Different-Email-Clients.html)

[邮件 html 页编写指南](https://my.oschina.net/u/4418120/blog/3576140)

[一文看懂前端怎么写HTML邮件模版](https://juejin.cn/post/6903138530370715656)