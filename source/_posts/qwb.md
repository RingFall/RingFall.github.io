---
title: 啪嗒啪嗒强网杯
date: 2018-03-24 18:10:37
categories: Blog
thumbnail: "https://s1.ax1x.com/2018/03/24/9qeSsJ.jpg"
---

icq这个比赛平台设计的人绝对是中二吧。。看起来很炫酷结果加载卡洗==还感觉乱糟糟的x（好吧窝可能枣就是痴迷性冷淡风格的直男程序猿惹x

从昨天晚上一直一会有电一会停电到早上，窝也是惊了，新老婆显示器开开关关的莫名心疼QAQ，然后一亮一暗的。。mmp哦

然后就是一整天坐在两个老婆前的划水（躺（然后其实没啥好写的。。。（不经意间博客已经全是乱七八糟的东西惹哭唧唧

每次这种比赛。。血槽亏空。。菜唧唧。。洗心革面。。

周日又水了安恒的月赛（躺。。几度怀疑窝这种老年人真的要继续吗。。。

想了想还是该振作，毕竟窝可是喵王嗷

### 签到

fb：不好意思，网速快就是可以为所欲为x

这签到是为了看有几个队做了的吗23333（好像就是

### welcome

不叽到是啥文件，看了winhex也不叽到

然鹅放到虚拟机里一下就看粗来了，直接有显示一看就是bmp的缩略图，binwalk一下

[![9qmPXQ.md.jpg](https://s1.ax1x.com/2018/03/24/9qmPXQ.md.jpg)](https://imgchr.com/i/9qmPXQ)

啥是PC bitmap喵喵喵？然后后缀加bmp用神器打开点点点就有啦~

### WEB签到

这签到。。。太皮惹吧

数组直接绕过两个还以为flag近在咫尺==结果第三个怎么也绕不过==

`if((string)$_POST['param1']!==(string)$_POST['param2'] && md5($_POST['param1'])===md5($_POST['param2']))`

查惹string强转，数组只能变成Array，前一个是绕不过哒QAQ

又查md5姿势。。0e开头只能在弱等于下，，数组又不可行，，米有姿势

结果很暴力。。。直接找两个md5相同的字符串。。ORZ。。google粗来 都是zlj超厉害的那个导师王小云，膜

然后试吖试，，找到的是16进制的，又要转换

py16进制转ASCII（2.7.6版本）： `'data without 0x'.decode('hex')`

然后直接脚本了。。总有种搞复杂了的感觉迷

```python
import requests

url='http://39.107.33.96:10000/'
cookie={
'PHPSESSID':'81g66k2a5didsdcaqqjd7m6aa5'
}
a=('4dc968ff0ee35c209572d4777b721587d36fa7b21bdc56b74a3dc0783e7b9518afbfa200a8284bf36e8e4b55b35f427593d849676da0d1555d8360fb5f07fea2'.decode('hex'))
b=('4dc968ff0ee35c209572d4777b721587d36fa7b21bdc56b74a3dc0783e7b9518afbfa202a8284bf36e8e4b55b35f427593d849676da0d1d55d8360fb5f07fea2'.decode('hex'))
data={
'param1':a,
'param2':b
}
f=requests.post(url=url,cookies=cookie,data=data)
print f.text
```

每次写个脚本总是把上次刚刚搞错的语法又搞错，上次记下的问题又忘记，老年痴呆ing。。。果然还是平时懒

![9qnbdA.jpg](https://s1.ax1x.com/2018/03/24/9qnbdA.jpg)

### Share your mind

讲道理。。。看了wp后悔洗周末没好好看这题了QAQ

虽然就算看上两天可能还是想不到。。但这个漏洞真的是看到过啊嗷嘤嘤嘤，平时看文章一眼掠过感觉好难收藏起来以后再研究的臭毛病啊呜呜呜呜呜呜呜呜呜呜呜呜

恩，以后再看看这题（光速打脸。。。

下次看到这儿记得去看！看！看！打洗寄几算了。。。

还有两道flask的。嗯。也以后看。

会记得的。坑在这呢。

