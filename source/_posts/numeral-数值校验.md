---
title: numeral-数值校验
date: 2024-01-02 13:31:20
tags: 工具
---

### 数值操作推荐使用numeral.js

numeral.js—一款比较好用的用于格式化和操作数字的js库。
官网：http://numeraljs.com/

Js运算存在精度丢失问题，例如0.1+0.2不等于0.3；numeral就是用来解决各种数字操作问题的工具库，github的star数近1w；还是比较靠谱的。

<!-- more -->
安装
yarn add numeral
引入
import numeral from 'numeral';
常用方法
将各种其他格式转化为数字
```
let myNumeral = numeral(1000);
let value = myNumeral.value();   // 1000

let myNumeral2 = numeral('1,000');
let value2 = myNumeral2.value(); // 1000
```
   
转化示例：
| Input| Value |
| ------ | ------ |
| numeral(974) | 974 |
| numeral(0.12345) | 0.12345 |
| numeral(’10,000.12’) | 10000.12|
| numeral(’23rd’) | 23 |
| numeral(‘$10,000.00’) | 10000 |
| numeral(‘100B’) | 100 |
| numeral(‘3.467TB’) | 3467000000000 |
| numeral(‘-76%’) | -0.76 |
| numeral(‘2:23:57’) | NaN |