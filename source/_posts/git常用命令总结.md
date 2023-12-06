---
title:  git常用命令总结
date: 2023-11-09 14:17:53
tags:
---

### 提交代码流程 
  1. 从 master 分支开出新分支 feature/example：**git checkout -b feature/example**
  2. 将此feature分支推送到远端： **git push –set-upstream origin feature/example**
  3. 查看此分支git状态：**git status**
<!-- more -->
  4. 查看分支改动的详细代码：**git diff**
  5. 将改动文件从工作区添加到暂存区：**git add .**
  6. 将改动文件从暂存区提交到当前分支：**git commit -m ‘xxx’**
  7. 5和6两步可以合写为： **git commit -am ‘xxx’**
  8. 将分支改动推送到远端：**git push**
  9. 将分支发到测试环境：先切到测试分支develop, 比较分支的文件差异 – **git diff feature/example**( *审查代码 防止出错* ) 再合并：**git merge feature/example –no-ff** 最后再 **git push** 推送到远端
  10. 分支发到预发或线上环境同上

### 撤回相关
  11. 5步添加之前想撤销所有提交：**git checkout .**
  12. 5步添加之后想要撤销提交：**git reset .**
  13. 6步commit之后想撤回：**先 git reset HEAD~1** 然后 强推到远端 **git push origin feature/example –force**
  14. 想撤销某个版本commit：**git revert -m 1 版本号** [参考：记一次git revert的经历](https://blog.justwe.site/post/git-revert/)
  15. merge到dev分支之后想撤回合并：先切到dev分支：**git checkout develop**, 查处要回退的版本号：**git log或者git reflog**, 然后 **git reset –mixed 版本号**  最后把reset改动推送到远端：**git push origin dev/master -f**<font color="red">(注意区分reset和revert的区别，reset会撤销此分支版本号x之后的所有commit，而revert会撤销仅仅此版本号的commit并作为一个新的commit)</font>
  16. reset后 后悔怎么办： **git reflog**查看reset操作之前的版本号mm，然后再次**git reset –mixed mm**

### tag
  * 查看：**git tag**
  * 提交：**git tag -a v0.0.1 -m 'project init'**，然后**git push origin v0.0.1**
### remote
  * 查询当前origin: **git remote -v**
  * 删除当前origin: **git remote remove origin**
  * 添加origin: **git remote add origin https://github.com/username/reponame.git**
  * 修改当前origin: **git remote set-url origin https://github.com/username/reponame.git**

### 其他
  * 查看所有分支：**git branch -a**
  * 删除本地分支：**git branch -d feature/example**
  * 删除远程分支：第一步：**git branch -r -d origin/feature/example**  第二步：**git push origin :feature/example**
  * 查看命令树：**git log –oneline –graph –decorate –all**
  * rebase: [rebase](http://gitbook.liuhui998.com/4_2.html)