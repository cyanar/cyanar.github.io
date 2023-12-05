---
title:  git常用命令总结
date: 2023-11-09 14:17:53
tags:
---

### 提交代码流程 
  * 1 从 master 分支开出新分支 feature/example：<strong>git checkout -b feature/example</strong>
  * 2 将此feature分支推送到远端： <strong>git push –set-upstream origin feature/example</strong>
  * 3 查看此分支git状态：<strong>git status</strong>
<!-- more -->
<p>4 查看分支改动的详细代码：<strong>git diff</strong></p>
<p>5 将改动文件从工作区添加到暂存区：<strong>git add .</strong></p>
<p>6 将改动文件从暂存区提交到当前分支：<strong>git commit -m ‘xxx’</strong></p>
<p>7 5和6两步可以合写为： <strong>git commit -am ‘xxx’</strong></p>
<p>8 将分支改动推送到远端：<strong>git push</strong></p>
<p>9 将分支发到测试环境：先切到测试分支develop, 比较分支的文件差异 – <strong>git diff feature/example</strong>( <em>审查代码 防止出错</em> ) 再合并：<strong>git merge feature/example –no-ff</strong> 最后再 <strong>git push</strong> 推送到远端</p>
<p>10 分支发到预发或线上环境同上</p>

* 撤回相关

<p>11 5步添加之前想撤销所有提交：<strong>git checkout .</strong></p>
<p>12 5步添加之后想要撤销提交：<strong>git reset .</strong></p>
<p>13 6步commit之后想撤回：<strong>先 git reset HEAD~1</strong> 然后 强推到远端 <strong>git push origin feature/example –force</strong></p>
<p>14 想撤销某个版本commit：<strong>git revert -m 1 版本号</strong> <a href="https://blog.justwe.site/post/git-revert/" target="_blank" rel="noopener">参考：记一次git revert的经历</a></p>
<p>15 merge到dev分支之后想撤回合并：先切到dev分支：<strong>git checkout develop</strong>, 查处要回退的版本号：<strong>git log或者git reflog</strong>, 然后 <strong>git reset –mixed 版本号</strong>  最后把reset改动推送到远端：<strong>git push origin dev/master -f</strong><br><font color="red">(注意区分reset和revert的区别，reset会撤销此分支版本号x之后的所有commit，而revert会撤销仅仅此版本号的commit并作为一个新的commit)</font></p>
<p>16 reset后 后悔怎么办： <strong>git reflog</strong>查看reset操作之前的版本号mm，然后再次<strong>git reset –mixed mm</strong></p>
</li>

<li><p><strong>其他</strong></p>
<p>查看所有分支：<strong>git branch -a</strong></p>
<p>删除本地分支：<strong>git branch -d feature/example</strong></p>
<p>删除远程分支：第一步：<strong>git branch -r -d origin/feature/example</strong>  第二步：<strong>git push origin :feature/example</strong></p>
<p>查看命令树：<strong>git log –oneline –graph –decorate –all</strong></p>
<p>rebase:<a href="http://gitbook.liuhui998.com/4_2.html" target="_blank" rel="noopener">rebase</a></p>
</li>