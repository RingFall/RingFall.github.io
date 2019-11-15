---
title: 小鲸鱼哒小仓库
date: 2018-04-17 20:33:25
categories: Blog
thumbnail: "http://www.ruanyifeng.com/blogimg/asset/2018/bg2018020901.png"
---

> “每次花了好大的劲终于解决了一个困扰自己已久的问题发现只是一个小小的粗心时，都会庆幸没有开口去问别人，同时觉得自己真的是太蠢了TAT”
>
> “可也有一瞬间啊，觉得自己呢，超级无敌厉害。”

先放资源：

- 视频教程： [IMOOC-Docker入门](https://www.imooc.com/learn/867)
- 菜鸟教程： [Docker 教程和命令](http://www.runoob.com/docker/docker-tutorial.html)
- gitbook： [Docker — 从入门到实践](https://legacy.gitbook.com/book/yeasy/docker_practice/details)
- 加速及仓库使用教程： [docker使用阿里云镜像仓库](https://blog.csdn.net/qq_30259339/article/details/52400673) （为啥窝的淘宝还是连的窝爸的支付宝吖23333，这它喵都能实名）

### docker

[![CnKqwq.md.png](https://s1.ax1x.com/2018/04/17/CnKqwq.md.png)](https://imgchr.com/i/CnKqwq)

从官网就可以看粗来docker的各种优点~

最基本哒：下载镜像->运行并映射端口->访问(->修改->提交保存->传仓库)->停止

### VMware

虚拟机里默认localhost居然是0.0.0.0

用ifcongfig（win里ipconfig）查看虚拟ip加上端口就可以在本机访问啦~

### dockerfile

由一系列命令和参数构成的脚本，这些命令应用于基础镜像并最终build一个新的镜像。

每个命令是分层的

### 卷挂载

方便于开发，直接把本机data或代码挂载在容器上运行

### compose

多个容器的配置启用







