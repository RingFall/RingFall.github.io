---
title: 像git一样思考~
date: 2018-04-16 14:40:20
categories: Blog
thumbnail: "http://rogerdudler.github.io/git-guide/img/trees.png"
---

之前有看git来着。。也就几个常用命令。。然后没咋用啊没咋用就又忘了。。复习复习（毕竟同性交友利器吖~

最简单的显然是[git - 简明指南](http://rogerdudler.github.io/git-guide/index.zh.html)

然后另一个很棒哒网站[Think Like (a) Git](http://think-like-a-git.net/)

觉得挺可爱的，还增加了一波词汇量，学习记录一下

- 图论：点和线|有向无向图|可达性
- References (local branch, remote branch, and tag) are points to commits.  创建一个分支的本质是一个40bytes的标识
- local branch references: `commit`, `merge`, `rebase`, `reset`|remote branch references: `fetch` ,`push`|`pull`  = `merge` + `fetch` or `rebase` 
- `Tag` will never change (unless you explicitly update it using the `--force`option)
- `git commit --amend` 将新的更改添加到之前的提交里
- `git gc` 垃圾回收，删除无法访问到的提交节点
- References Make Commits Reachable. 分支=一个节点的引用/指针|创造分支=可能想回到这时状态
- 防止merge不如意的两种方式：scout(Create a new branch to test merge, and switch to it)|savepoint(Create a new branch to use as a savepoint, but don't switch to it.)
- `git log` -> `git reset --hard xxxxxxxx` 
- `git rebase foo(first_this) bar(then_this)`

![img](http://think-like-a-git.net/assets/images2/before-rebase.png)

rebase 后：

![img](http://think-like-a-git.net/assets/images2/cherry-pick-qua-rebase-example-endpoint.png)

以上。

最后下了个sourcetree，把以上都扔了x