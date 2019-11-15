---
title: Q&A
date: 2018-07-24 22:26:08
tags:
thumbnail: "https://s1.ax1x.com/2018/09/17/iZaESs.jpg"
---

ubuntu里除了经常各种目录没权限之外apt下载时经常会出现下面的报错

```
E: Could not get lock /var/lib/dpkg/lock - open (11: Resource temporarily unavailable)
E: Unable to lock the administration directory (/var/lib/dpkg/), is another process using it?
```

- 找到并且杀掉所有的apt-get 和apt进程

  `ps -A | grep apt` `sudo kill -9 进程ID` 

- 删除锁定文件

  `sudo rm /var/lib/dpkg/lock` `sudo dpkg --configure -a` 

  或

  `sudo rm /var/lib/apt/lists/lock` `sudo rm /var/cache/apt/archives/lock` `sudo apt update` 

***

FxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxK!!!!!!!!!!!!!!!

今儿想爬个网站，哼哧哼哧写了个框架一运行，报了一大堆错（微笑

定睛一看源头是import requests？？？？2和3都是？最后报了个认不得的错？？？

`python2: 'module' object has no attribute 'maketrans'`

`python3: cannot import name 'Template'`

神奇的是，窝直接在控制台import就可以？？？就运行这个文件时不行？？？

~~理性分析一下好像是除了路径没啥不一样~~ 胡乱搜搜米有结果，突然看到一个回答是是不是当前目录下有string.py，呵呵一声哪有这么撒的，继续搜ing。。。

然后。。切到窝的可爱的jy文件夹下的时候。。。真它喵看到个string.py。。。眨了眨眼。。。还在。？？？

哭惹！呜呜呜呜呜呜呜呜呜呜呜呜

***

emmmmmm第不叽到第几次hexo g -d报错

以前么各种情况都有，空格啊中文符啊

然后sublime里标红的都是骗喵的。。。最后发现这次是两个大括号不行。。。着实心累

喵生最累的就是哒环境和debug了吧

***

遇到好多次解决不了的在pip install时 `SNIMissingWarning` 和 `InsecurePlatformWarning` 的报错

解决方法：

- 弃疗，直接用3去了
- ~~搜出来是 `pip install pyopenssl ndg-httpsclient pyasn1` 和 `pip install requests[security]` 都系假的。。还是报同样的错~~ 
- 升级到Python2.7.9以上，直接去官网下载release for windows然后覆盖安装就好（窝嗦升级教程怎么只有linux的x

***

docker的问题。。（Ubuntu里）

- 记得干啥都要sudo
- `Cannot connect to the Docker daemon. Is the docker daemon running on this host?`  但是docker明明都有的啊？ `service docker start` 一下，虽然窝验证好像没成功？但系可以了orz

***

hexo的yml用空格就憋用tab！！！血的教训！

***

anaconda装module用anaconda prompt小黑框鸭~

（所以你在本机搞啥啊摔！

***

jupyter notebook默认打开的什么鬼路径

[修改方法](https://www.zhihu.com/question/31600197/answer/90214029) 