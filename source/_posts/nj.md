---
title: 江苏省xxxxxxxxxx技能大赛
date: 2018-09-16 20:09:32
tags:
thumbnail: "https://s1.ax1x.com/2018/09/16/iZSEJx.jpg"
---

> 你的笑像一条恶犬，撞乱我心弦。<p align="right">——花粥 《盗将行》</p>

名字太长而且去了才知道，记不得了x

人生中的第二次AWDx，终于不是一脸懵逼地强行删站了哭

和上次没有web手的区别是，这次有个前一天晚上电脑蓝屏然后重装的居队友x，比赛的时候还嫌窝凶？？？啪叽！wh还嗦要学他多嗦发，嗦个屁屁啊。不过wh关心能力max啊23333，给窝占座、让hph穿他衣服，而且窝好喜翻他的那个外套和手表x，好想问是啥牌子啊（捂脸，车也不错hhhh

嗦肥比赛，感觉窝这种宅加闷葫芦就不适合组队出去扣唉扣，感觉他们那种交♂流到半夜的肯定很有收获2333，窝就不行x

首先赛前一波骚操作，得到了大致题目方向，然后次了个晚饭！就在窝以为没饭吃要自己半夜点外卖的时候！南京菜！炒鸡和我胃口啊！都是江苏咋差这么大呢哭

早上走了好远好远去计院，南理工好大啊，在南京不算郊区还有这么大的地是家里有矿嘛？（在门口还看到了重庆鸡公煲，流口水ing。。）首先AWD混战，这次准备的稍微充分一些，所以虽然连接shell方式有点特立独行还是用窝的看起来很好用哒新工具连上惹，改了密码，两个PHP的站down了源码，自动搜索一波，记录了路径然后补了洞。坑的是，别的队的ip没给，所以wwb就在那扫，扫了半天都只有各队控制主页喵喵喵？问了也不给网段。。。于是就在这僵了好久。

后来好像是瞎jb试出来的，然后找出了规律（赛后问好像大家都是猜出来的，因为神它喵端口在5000，而且访问网站还得加路径。。。），找到之后先是用config.php的马试了一波，大概三个队能连上，然后！突然就一波被打！一看是那个看不懂的103！看了半天没找到php或者py文件还天真地以为是pwn（扶额，后来发现了站在app目录下，，是个python站，哭惹，然后就没心情看101的其他漏洞咋打了，跑去死磕103

因为是Python各种找洞工具都用不上了，肉眼查杀启动（然鹅依旧看不大懂，硬看叭。发现一个upload，改不来。删了。还有个download。也删了。然后wwb在那和一队py半天，，终于py来一个 `url/%7B%7B%20''.__class__.__mro__[2].__subclasses__()[40]('./flag').read()%20%7D%7D` 赛后一查是一个jinja2代码执行漏洞，可以报错出flag，get一波终于不是负分了嘤

然后就没有然后了。。。两个小时后来又加了半小时，flag半小时刷新一次，最皮的是窝都把各种关了准备收拾收拾次饭惹，最后几十秒它刷新了？？？？？？？？？？mmp哦？？？皮?.jpg

中饭可还行，萝卜汤很暖鸭，橘子也比窝买的甜到不叽到那里去了x

下午渗透，又是不给ip，日。不过这次倒是有了经验很快就猜到了：）

第一个是一个windows主机的PHP cms站，hph一个永恒之蓝直接administrator了，结果只找到一个桌面的flag，进去了也不造干啥 / 第二个是个typeecho博客，后台admin admin进去一个flag，后台修改上传允许的文件后缀然后传马根目录一个flag，然后找到了数据库密码然鹅一直连不上，应该是没权限可是不会提权，于是第二个就没进度了 / 第三个第一下御剑扫出robots.txt下一个flag，结果那时候交上去平台一直嗦ip不合法，问了是他们的问题，看那时候情况应该是窝第一个问的，感觉因为这个问题错过了一血，虽然一血也没啥奖励叭x

此时好像有一瞬间的第一，wwb还空的在那里拍照留念:)，然后就有点萎了（发现我每次都这样，有思路就超快后面越久越没动力瘫。之后就是艰难的探索，后两个站一直僵在那只能从第一个里下手，但系只有hph那用着极度不称手的mac连着，所以就在他那的phpstudy各种找数据库找站，数据库里没找出来，但它找到了第一个和第三个的后台密码，然后两个flag，最后又瞎试出来一个貌似是内网的，说好的搭建vpn也没哒，就瞎看xxx，然后就结束了。

肥来的时间超紧脏，前一天还想和盐喵富婆约饭，，还想去新街口次饭，，最后连买个肯德基都差点来不及，这还是在骑了车代替南理工里超远的路的情况下==

肥来之后又是刷OJ自闭时间，不过能出去一趟肥来还有个周日假缓一缓还是好点苏糊哒~中午刷完OJ躺着准备碎觉的时候在网易云发现一个超棒的为你读诗集合！不仅有窝居居bei宇袁朗队长史今班长还有各种超有名作家演员歌手！然后就不知道为什么地哭了好久。诗什么的，真的太美好太温柔了啊。

[![iZCDkd.md.jpg](https://s1.ax1x.com/2018/09/16/iZCDkd.md.jpg)](https://imgchr.com/i/iZCDkd)

啊念的是背影，打成父亲了。听的时候就想起不久前看的我们仨了。。。前面那段写钟书和女儿相继离去真的是，，最后是在文献检索看完那部分的，，就算在上课都哭得不能自已，明明在有人的情况下一般都会忍住的，，应该只有看忠犬八公和这次是在课上就控制不住的了。天呐。杨绛的每一个句子里无一不是一个老人那样子深切的害怕失去，想要抓住却又无力，弱小的思念和关切啊。怎么忍心呢。怎么能呢。这样的万里长梦，真实与虚幻不可分割，这样的寻觅与迷途。我靠。太悲伤了吧

另外发现和某些人说正事说着说着就会开始聊人生，各种压力真的太鸡儿真实了。（哪怕窝自己一直看起来非常佛性，都是假象吧可能

这个就到这儿叭，去更新安利惹！明明看了好多但系好久没更惹诶嘿嘿
