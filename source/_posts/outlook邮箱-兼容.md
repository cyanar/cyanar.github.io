---
title: outlook邮箱-兼容
date: 2024-01-02 14:05:02
tags: 其它 兼容
---

### Outlook邮箱兼容性记录

> Outlook的发布由于使用了Word的渲染引擎代替了以往基于IE浏览器的Html页面渲染，给邮件设计者带来了很大影响

<!-- more -->
* Outlook 2007-2013 不支持图片的 margin 与 padding 样式，必要的时候可以尝试 hspace 和 vspace 属性；
* 所有可以连写的样式全部拆开写，例如`padding：10px 20px`，要写成`padding-top:10px;padding-bottom:10px;padding-left:20px;padding-right:20px`
* 行数很多的文本记得加上`word-break:break-all;`
* outlook不能识别`!important`；
* **img width 和 height 属性**一定不要加上单位;因为加上单位会使一些版本的 OutLook 无法正确识别，导致图片显示使用实际的宽高而非我们设置的;
* 避免使用div标签；
* span标签使用padding无效，只能先用td标签或者使用`&nbsp;`代替；
* 其它--[outlook tricks](https://www.lmlphp.com/user/62535/article/item/870437/)

#### 补充--Outlook 2019/2023踩坑:
* div和tbody标签`background`及`background-color`失效；**td**标签支持`background-color`;
* 不支持CSS3，所以`border-radius`这一CSS3属性不生效;
* 不支持`min-width`；宽度使用**width**;

* 会自动给td标签添加上下padding;

* 字体color设置opacity失效，只能使用色值;

* `hr标签`在outlook不同版本展示不同，只能用**table**模拟分割线；

* 属性后不要加`!important`；outlook不能识别会影响属性的正常显示；

* 如果使用了*line-height*属性，需加上`mso-line-height-rule: exactly;`(OutLook 有默认最小行高，使用OutLook自定义属性mso-line-height-rule:exactly（该属性只在块元素上有效）来取消限制);

* 添加`meta和body`后，可解决特殊字符如© 显示乱码问题；

#### Outlook 2021踩坑:
* 样式继承问题—-html邮件中某些属性的继承可能失效，比如`font-family`,若想改变字体，所以至少每个 table 中都要指定`font-family`；

* 白线问题--`<table>`里套`<table>`有的td后面会出现一条白线，如模板EML_100000038:
![pic](https://cloudstorage-oss-sit.oss-cn-hangzhou.aliyuncs.com/zeekrui/255a9e75652b41d3b35f91b98209bd3d.png)

**解决方法是修改td的line-height为偶数**:
```css
style="padding: 8px 16px;font-size: 14px;line-height: 20px;"
```
#### Outlook 2016踩坑:
* 样式继承问题同Outlook 2021

* `hr标签`在outlook不同版本展示不同，用**table**模拟分割线在2016中会高度异常；解决方法：用td来模拟hr时要加 `&nbsp;`，注意要用`ghost table`，因为在gmail-IOS客户端 `&nbsp;` 会渲染为一个空行；
```html
    <td style="border-bottom: 1px solid #E5E6E7;height:1px;line-height: 1px; width:100%;mso-line-height-rule: exactly;">
      <!--[if mso]>&nbsp;<![endif]-->
    </td>
```

#### 参考
[Fixing White Lines in Outlook](https://www.actionrocket.co/email-design-review/white-lines-in-outlook#:~:text=Solutions,-Okay%2C%20so%20you%20have)

[OUTLOOK2016邮件样式和inline图片兼容性等问题解决](https://www.cnblogs.com/slankka/p/13914414.html)

[微软官方文档--word渲染引擎对HTML兼容支持](https://learn.microsoft.com/en-us/previous-versions/office/developer/office-2007/aa338201(v=office.12)?redirectedfrom=MSDN)