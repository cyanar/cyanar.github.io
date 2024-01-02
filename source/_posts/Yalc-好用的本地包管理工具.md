---
title: Yalc-好用的本地包管理工具
date: 2024-01-02 10:51:22
tags: 工具
---

### npm link 或 yarn link
npm link 或 yarn link 实际上在全局包路径（Global Path）下创建一个软连接(Symlinked)指向你的 npm 包
然后在业务工程里通过软链接，将全局的软链接指向到 node_modules/[package]
这个往往也是需要两个步骤
<!-- more -->


* 在需要生成软链接库下执行 npm link，在业务工程下执行npm link [package]
* 在需要生成软链接库下执行 yarn link，在业务工程下执行yarn link [package]

**此方案缺点：**
影响node_modules中原本的依赖包;
软链接和文件系统引发的其他各种奇怪的问题； 
### 相对路径或者绝对路径使用
比起 npm link，我们还尝试过使用相对路径或者绝对路径进行引用。
将业务代码中的 import 和require所用到的地址，从在 node_modules 里检索改为真实的物理地址。例如：
```
import { Button } from 'good-ui' 
```
为了调试，强行改成了绝对或者相对路径 
```
import { Button } from 'C:/codes/good-ui/dist'
```
**此方案缺点：**
需要频繁改业务代码，这既麻烦又危险（路径有可能进行修改，在 git 提交代码的时候，引用路径忘记修正回来则其他开发者无法正常使用）。
### 为什么要用 yalc 
yalc 可以在本地将 npm 包模拟发布，将发布后的资源存放在一个全局存储中。然后可以通过 yalc 将包添加进需要引用的项目中。
这时候 package.json 的依赖表中会多出一个 file:.yalc/... 的依赖包，这就是 yalc 创建的特殊引用。同时也会在项目根目录创建一个 yalc.lock 确保引用资源的一致性。因此，测试完项目还需要执行删除 yalc 包的操作，才能正常使用。
整个过程相对于 npm link 会更加繁琐一些，要经过发包、添加依赖，结束后也需要做清除操作，但也正因此才避免了 npm link 的一些问题。
传统 npm link 依赖表如果出现 N 个依赖，则在使用 npm link 包的时候，需要一个个的去安装，而对于 yalc 来说无需一个个去安装依赖，在项目目录下直接进行 npm install 即可。
### yalc常用命令

全局安装yalc:
```
npm i yalc -g 或
yarn global add yalc
```

在插件包[package]目录下执行
```
yalc publish
```

在项目目录下执行
```
yalc add package
```

如果你修改了插件包里的一些代码，执行
```
yarn lib && yalc push—会触发 HMR
```

移除依赖-在项目目录下执行
```
yalc remove package
```

其他用法
```
yalc update package # 更新依赖
yalc remove --all # 移除当前包里的全部yalc依赖
```
。。。