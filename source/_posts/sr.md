---
title: Deja Wu
date: 2019-07-15 10:16:11
tags:
thumbnail: ""
---

## 6.2 - zoom0.1

使用 [Figma](https://www.figma.com/file/IGO7vwtu1rdsEbuZAmXlVbAa/Deja-Wu?node-id=0%3A1) 介绍了情景：

- video等 - 用直觉keyword搜到
- email/文件
- 搜索后对应的最终复制的text/截图
- 社交网络  ~~（需要登录访问？还是直接快照？）~~ 
- 弱数据类型（如邮件里有xxx加冒号）

重现搜索/浏览历史keyword和行为

目标：usefulness、usability、通用化（理解+规则）、直接给出用户想要的信息

学习 Fauxbar 的框架做 search bar -> 封装模块 -> 数据交互

## 7.12 - zoom0.2

最终实现形式为打开新tab时出现search bar

[formative study: summary](https://docs.google.com/document/d/11t0Rk0vp-PCFaAntSToLkglzHWr-TaHtaVcaVAxzx-E/edit) / [Study Synthesis](https://docs.google.com/spreadsheets/d/1gWbMYzXUkuTQTIo_kGxOHRz7OAZ5yb5HYk7bXZl1-Gs/edit#gid=0) 

整体如何以用户需求为导向实现，在用户浏览时捕获用户注意力点和行为来确定（email栗子：只会想搜看过的），安装时仅通过history搜集，安装后可在浏览时搜集

如何普适性地分析网页：（research哒意义：结构化认识用户浏览记录，抽象出真正感兴趣的）

- 用户想要网址还是数据 -> 对数据类型不需要有强的认识
- 网页和描述信息的共性

切入点：重复访问，简单逻辑

分析时可能会用到nlp、分词之类的，具体在开发时会涉及

不要局限于细节，要对用户motivation有宏观认识

之前repo的后台可以迁移，再进行拓展

每天记录吖（工作都是小模块），重点：描述好进度、沟通好问题

（可以学学react）

截图时可以直接给出dom tree中text

## 7.15 - zoom0.3

介绍根据用户调查确定的重新搜索难度分类

栗子（嵌入的video，keyword和标题不对应，可从最初query入手；共享文件和已删除post：几乎不可能重新搜到）

~~ps. 听说了一个好东西：[trello](https://trello.com/) 这不就是窝一直想找的防拖延防懒癌ddl管理嘛哭~~ 

## 7.16 - 0.未参加

不叽到嗦了啥qvq，在群里发了个图，~~待更新~~ 

![eCYv0U.jpg](https://s2.ax1x.com/2019/07/22/eCYv0U.jpg)

## 7.17 - 1.0

delta体验满分，还在灰机上拍到了和月亮肩并肩的皂片！开心x 转机拿行李也不是很麻烦，除了过海关真的排了好久的队，然后国内飞机的登机口最后变了之外，其他都很顺利鸭~

然后就遇见啦Patricia，真的好热情qvq，看了一眼匹茨堡downtown，然后就进入了山区x

买了超大一片的pizza肥去加热味道真的还不错，然后见到啦Sally~一个晚上拉了四坨x

## 7.18 - 1.1+zoom1.1 

根据不同需求实现形式的三种分类

完善了table和流程图

讨论了下周二前任务具体实现目标

然后前端就给那个js哒expert惹？那窝干嘛鸭

总之就是看看怎么用api tracking，然后怎么个算法和怎么存储，然后返回显示啦~ ~~（说起来真的好简单qvq，结果API都看不懂~~ 

---

和Patricia逛超市！买了一整箱blueberry！还有好多次的！QAQ！太爽了叭

早饭系柜子里原来哒麦片，中饭系昨天剩下哒pizza和刚买哒cherry和椰子水！比自来水不叽到好喝到哪里去惹嘤嘤嘤！晚饭系squash和牛肉，为了把握熟的程度寄几煎哒！

下午Patricia开车送我去tepper quad见面后就尝试惹第一次坐车肥去QAQ。Patricia安利的APP时间一丢丢也不准，然后不报站？喵喵喵？？枯了，只能看定位预判寄几到哪了

晚上坐在床上一边zoom一边次一盘蓝莓真的是美滋滋x然后就碎着了！碎到九十点叭，起来洗了个澡就十二点了？然后明明是下楼准备嗦goodnight的结果先是逗Sally玩然后变成了装Patricia新买的汪窝~虽然很简单蛋窝力气小啊x，不过还是完成啦！毕竟窝系engineer鸭~然后就被夸xN~

## 7.19 - 1.2

Patricia因为惊叹于窝的聪明才智(?)给了一个Nick name: fighter pilot，简称fp，为啥窝总觉得是flappy pig啊233333333333

早上次了昨天买的嘎嘣脆的麦片！好次嘤嘤嘤，中午带了水果去（虽然中午才去x），晚饭那个菜炒的焦焦的吼吼次鸭！但是那个鸡翅窝喵喵喵？画的那么好看结果又酸又辣？？？而且根本不是烤翅嘛QAQ

---

因为没了前端的活所以突然的迷茫？就看了下另一个小伙伴画的流程图？感觉和窝想的不太一样啊qvq，然后就各种问题和mentor嗦了一哈，正好嗦到NER，就让窝搞语言处理这一块，窝一看这不就是分词嘛~~，大创凉凉预警~~ 用ml在用户端建模型肯定不现实啊，要是还要server也好麻烦鸭，所以就踏上了直接找API的道路，然后窝给他看窝找的NER，他看了一哈嗦用google cloud的nlp API，因为它功能全。

~~然后窝看了一眼不就是加了ner之外的什么词性标注之类的吗？？你枣嗦窝直接找个不仅仅是ner的啊？不是你嗦要ner嘛。。。咱也不敢反驳qvq~~ 就丢了两个链接嘤嘤嘤

于是又得去注册google cloud，神它喵找中国找了半天最后确定没有？？？随缘吧。。。有信用卡就行

然后发现只用这个做nlp的API也太可惜惹！这个看起来好像灰常全能啊！还有云端函数和存储，明天去给他们安利一波~

然后因为在那没信用卡，所以就枣枣的肥来惹，在门口遇见了来自越南的nlp大佬？在Patricia的督促x下和窝愉快地聊天？给了我一些申请的建议然后窝发现窝好像都已经无能为力了吖QAQ，然后发现窝比Patricia更能get他的笑点？23333

哦对，忙完记得加linkin

肥来之后就发现mentor发了微信让窝赶紧调qvq

google cloud还是友好顺利地调出来了，然鹅尝试那个fetch的函数就一直米有返回哭。哦对，然后终于搞明白deja wu他们原来已经有的代码是啥了，就是把webpack用在chrome extension开发上，可以hot reload，搞明白了就苏糊了（瘫

## 7.20 - 1.3

早上四点醒来调环境你能信x

而且居然一整天下来还是和平常一样的困度x

---

第一下又是开始整理进度？总之分了一下各个方向？

[![eCttAg.jpg](https://s2.ax1x.com/2019/07/22/eCttAg.jpg)](https://imgchr.com/i/eCttAg)

- region of interest
  - spatial
  - cursor
- tracker
  - click
  - highlight/copy
  - screenshot
- query
- navigation graph
- NLP
- storage
  - key - url?
  - visit: time/number
- ranking

然后就整nlp API返回后的处理呗，本来想研究研究高大上的句法依存树？然后嗦不用qvq，于是就简单地把形容词加名词xN的这种短语找粗来就没惹x

还有就是有冒号那种，为了generalize窝就写一起了。最后返回的是一个数组，如果有冒号，值就放在数组最后，前面描述如果简短就直接进数组，如果长正好是按之前分析句子的流程抓出来放进数组。

然后发现在xhr函数外是无法获取xhr的改变的，因为是异步吖！外面执行完了函数还在请求吖！所以应该在函数里面返回哒~

另外：求求你憋再忘记写var了嘤嘤嘤

---

肥家做公交的时候终于！终于有一次在正确的车站下车惹！！然后就鸡冻地在三岔路口走错了路？qvq

晚上又装了个汪汪的小栅栏，每次次饭Patricia都会一直和窝聊天qvq，然后窝就次的更更更慢了x，吐槽川普啊，介绍她的girlfriends啊，blabla~

晚上本来想直接继续工作的，结果一碰到床就碎了嘤嘤嘤x

## 7.21 - 1.4

等了一个小时公交车！要不是那有个粗粗的电线杆窝就能在pitt热烈的阳光下成为喵喵干了QAQ（总之每天等车都会有种今天不运营的错觉x

喵生好艰难嘤嘤嘤

枣饭次完后Patricia居然也这么早起了？2333然后让我看newspaper上关于China的新闻？？惊了，还真都是狗屁x明明是China帮助别的国家建设一定要嗦有所企图？还控制世界？？还不如担心一下哪天本喵毁灭世界呢！还red scare，应该系喵喵scare！嗷~

愚昧。没话嗦x。不过报纸大概都这样叭，哪哪都一样x

幸好Patricia有一颗求知的心吖，还天天夸窝，窝可能这一个月后就上天了，walk into sky鸭23333333

---

开了一个新repo，然后窝在里面测试了一下发现返回时好像只有已知数组个数时能赋值emmmm

先commit叭x拿出多年没用的sourceTree~

下午摸了个session存储结构的伪代码，不用测试不用debug就是爽QAQ

然后在板子上画吖画，因为窝想的是直接索引前一个网页，结果Micheal嗦还是得有session的概念？因为最后的搜索是reverse的，行8

---

今天晚上去成都gourmet次饭饭！嘻嘻

然后就storm+flood？？？原来中文名叫老四川？？？枯了，这个暴雨真的是和那次被困徐州有的一拼

## 7.22 - 1.5

另一个小伙伴去downtown爽了？

于是窝一只喵在wean hall受冻QAQ

因为周二的目标的问题就先不写session了，然后是剩reverse和roi在content和background间传递和nlp处理再存储这两块，所以就写后面这个呗，前面那个又要看库x头大QAQ

第一下又有bug，天天de也太惨了叭，他还怀疑窝会不会de，窝。。。嘤

最后直接title还是tab数组改了

后面这个也要看函数，不过还行就直接可以work，然后本来想的在content里直接nlp结果因为content是直接在当前页面执行的所以会有corb跨域拒绝可还行，然后发送到background就可以啦~然后就是调调调

晚上等整合一下listener的handler

---

Patricia严肃地讨论了教授的问题，QAQ窝也想问啊，但是咱又不敢x，怂洗窝算了

## 7.23 - 1.6+zoom2.1

周二！第一个[Deja Wu Milestones](https://docs.google.com/document/d/1eyhijccVxJxD-lPIsRnP6KRDWdxyvDHw-DZBEdOGBAc/edit)！

早上Patricia计划了她的invitation。okokok

中午第一次吃外面的东西，7%tax+15%tip怕不是要吃穷我，再次感到选择homestay是一个多么明智的决定qaq

---

早上先是把长句和短语分开，加上标点，调updata存储时发现会overwrite，于是college就来调吖调，

最后整合好了两个listener刚好他也调好了

晚上zoom了第二周目标~

- storage转到firebase
- roi修改
- gmail
- key_value模糊搜索
- Associative memory
- fetch all associate memory
- Frecency + JS-search 
- UI
- error

---

commit前要先pull一下master！

## 7.24 - 2.1

TODO：

- 接收LinkedIn √
- 加stopwords，两个存储前 √
- 整理昨天记录 √
- roi找办法 √
  - viewport 部分包含修正
  - contain_English_letter 前端空格修正
- 把impliData放进index测试 √


## 7.26 - 2.3

## 7.26 - 2.3

## 7.25 - 2.2

- fix roi 重复 problems √
- gmail api
  - integrate 一定需要inject到dom里，无法作为content script执行 （Micheal√）
  - content
  - attachment
  - from
- 处理冒号key_phrase（等storage出来，目前firebase凉了23333333）

## 7.26 - 2.3

- capture roi without scrolling √

  窝惊了，这个[滚动](http://www.runoob.com/try/try.php?filename=tryjsref_onscroll)事件居然是按滚动幅度算次数的吗？？窝嗦怎么滚动一次执行好几次scroll，枯了x

- gmail （email address, email text, subject, attachment url）

  DOMEmail还是没法传，等fix再看qvq

---

去fallingwater！开心！

然后又是下雨，真的是falling water嘤嘤嘤

太豪华惹，总是会幻想要是当初真的学了建筑，会不会比现在搬砖的样叽有哪样哪样的区别呢x

好想住在深山里吖qvq

## 7.27 - 2.4

- YouTube 不一次性加载 √
- gmail text √
- 时间里也有冒号咋办鸭 用正则先取出来 √
- entity：时间，地点
- 怎么提取key_value鸭（冒号；nlp）
- 还要区分roi大小吗
- 感觉重头开始惹QVQ

---

中午的鱼好好次鸭嘤

上次觉得超好次的花菜末没那么好次了QAQ，一定是炒的不够焦x

## 7.28 - 2.5

枣上走过来的时候一个骑车哒和一个跑步哒和窝打招呼惹！嘻嘻

真是神奇吖，明明微笑只要微微牵动一下嘴角的神经，蛋却可以给寄几和他人带来那么大哒喜悦~

中午的印度菜好可怕啊QAQ晚上的红扁豆也有点鬼畜x

---

最终获取：

- 句子/段落内key_value（需要node确定看没看 -> 需要innertext中换行确定段落 -> entity找出value，key为整个段落）
- url的描述（所有innertext？如何删去导航栏之类的：innertext中短语占一行，innertext中本来就只有body里的，米有导航栏好像；email结构不同，email能用node吗）

新问题：

为了YouTube那种慢慢加载的改了extraction getAllNode之后node的seen flag就没用了QAQ

解决：

把nodes全局，只做更新

loaded突然粗线不了了QAQ竟然是网页加载太快惹？

如果用innertext那在innertext里也加flag？

还是区分出初始化的函数叭，页面加载时初始化（YouTube可以是在extraction里另加个判断），初始化为innertext分段

extraction逻辑：获取textnode -》 更新textnode（不在innertext里的不要，小于20字符不要） -》循环textnode按顺序匹配paragraph -》将匹配好的paragraphs传给bg

## 7.29 - 2.6

中介居然嗦窝的总结很详细23333，应该像Patricia嗦的那样写today is a good day. The END.

选座位必备：靠背，温暖，旋转，软垫，插座x

---

- filterImportantNodes 第一下想的是sidebar不在body的innertext里，结果发现都在 -》 然后发现都在innertext的最后，就想通过前后node的index间隔差大小来取舍，但是想到要是他已经划到最后了那sidebar content的index就直接在正文文本的后面了依旧无法去除 -》~~所以最后还是要看长度？~~ 或者设个判断的flag和已经发送过的flag合并起来叭 √

todo：

- optimize init √
- important √
- nlp提取entity key_value
- roiHandler还要留吗QAQ，都系爱写粗来的怎么舍得删嘤嘤嘤
- 存

---

TODO更新：

- paragraphs直接存textinterest √
- 修改不要的代码和命名规范 √
- key_value: 词_entity描述+textinterest中index √
- gmail区分获取所有innertext
- 看YouTube情况

## 7.30 - 2.7 

早上安慰了一波Patricia搞得她热泪盈眶然后想叫hai天天接送窝肥家了尴尬x

---

昨天晚上调到凌晨终于调好了gmail的get innertext（主要问题就是在index里只能抓到加载前部分，在inject里抓到的又米有分段，真的头大x喵生艰难嘤嘤嘤

好的新的一天新的TODO：

- 存储 √
- important还有问题，还是不能直接用差判断叭果然 -> 判断字体大小 ：在node处getTextHeight -> 打分（感觉不需要） -> 怎么用呢

找出长句（主体）的分数，高于这个为重要 √

---

mentor居然想把它搞成聊天机器人的样子x窝惊了，那是不是意味着离我的大创更进一步啊23333333

## 7.31 - 3.1

虽然写3.1但好像这周二并没有milestone？

但还是分隔一哈好有点时间概念，不然天天debug不知今夕何夕x

Garmin！窝的Garmin到惹！调了半天表盘，都好帅啊呜呜呜x今天走去学校试一波运动功能嘻嘻

那么今天干啥呢x

测试各种网页调各种bug

- 重要大字短句没存 -》更新：background收到的都会存，只在content过滤 √

- 在数组里找array的方法：

  `allTextNodes.find(o => o[0] === newNode.nodeValue)` 

- newNode和not include还有bug，去凉快有空调的地方调叭x窝怕电脑爆炸惹

墓地环境也太好了叭，完全一个超大的公园啊x最重要的是没人就很苏糊嘤嘤嘤

去了target，感觉也没啥可买的唉

---

又出bug了，虽说明天mentor嗦是休息，但寄几写的bug总得寄几调叭x

- find函数有问题 全等于undefined一夜之间不好用了？改成了直接非居然都有用 √
- 打分那个数组不ok 改成只读取数组里第一个值叭 不是数组就怎么都读不到x √

## 8.1 - 3.休息

中午和Patricia以及她的bestfriend一个中文老师一起逛了cemetery ~~好像不应该用逛2333~~ 

唉乐观真的是太重要了呜呜呜（没错窝嗦的就系窝x

---

回来继续debug叭

bug总是会调粗来的！冲鸭！

前两个算是改好了8

新bug：

- loaded多次时就会初始化多次？然后就会重复发？ 不会经常粗线，还行x （看了一下bg的发送逻辑因为title变了？
- YouTube不管打开哪个视频还是主页url都是判断的一样的x 不过存储的时候不一样就行
- YouTube的viewpoint又有啥问题？？？咋不太ok啊，每次都是只有第一下刷新的时候有用，滚下去鲧肥来或者换视频就都不行了x（所以为啥换视频console不刷新捏QAQ）


---

target逛了一个小时啥都没买x

可能是澳洲的教训叭x ，唯一一个有点心动的小板子一看made in China就有点丧失兴趣了，回来tb一搜虽然没有一样的但是发现了新的好东西！

## 8.2 - 3.2

要不要换老婆买小水果鸭x 这轻薄本天天装洗窝能咋办呜呜呜

早上正准备粗门mentor嗦可以下午再去聊进展，幸好磨蹭着磨蹭着就没出2333

去之前：

- 狂测，尝试fix，总结症状
- 这周末要开始新feature了 所以最好对现在的代码有个比较好的全局了解（主要就是存储这边的firestore + 上层对firestore存储的的load + background和content之间的通信）

okok正好虚心求教一波，窝为什么这么菜嘤嘤嘤

---

nlp - bug：

- YouTube长时间操作问题（究竟系为森莫console不刷新）

djw - bug：

- 怎么搜索出现的全是once copied?哦也有url，但窝好像没copy过啊喵喵喵？copied是哪来的？object里有吗？
- 顺序咋排的。。
- ~~小箭头有点丑咳咳x~~ 
- 说好的存在本地捏x，firebase又花钱又会有privacy的问题叭x，第一下为啥要换这个来着？不仅仅是用户的privacy还可能会是我们firebase的安全问题，要是有恶意用户写入啥恶意信息注入篡改别人的记录或者就是一直写入咋办x （Stack Overflow上嗦 [因为是nosql所以不容易受SQLinjection](https://stackoverflow.com/questions/48377034/sql-injection-in-firebase?rq=1) ?那MongoDB可能是个假的nosql？）看了一下还是得先 [过滤](https://github.com/firebase/firebase-admin-node/issues/317) 一波恩

代码问题：

- [setInterval](https://www.w3schools.com/jsref/met_win_clearinterval.asp) 只为了监听title加载？为啥在bg？为什么要设attempt？ √

其他：

- important size为什么是数组才能读？为什么窝更新为空然后push就读取不到？

总体感觉挺臃肿的。。。但还能处理的挺快也是绝了，js-search 6鸭？

---

meeting的肥答：

- YouTube网站特性就是这样
- copied目前是第一个interest
- 顺序还未排，未来会做title优先算法
- ？？？他们小水果好像没有丑丑的箭头？枯了
- 目前测试阶段不考虑安全问题x 换firebase是因为local有限制
- bg可以一直运行，content得加载，所以在bg发送信息直到content加载完成返回收到，但是又不能一直发所以设attempt

---

meeting的更新：

难道PhD就系天天否定自己之前的想法嘛？？让我们休息了一天嗦要下一个阶段加别的feature了结果meeting一描述——

这不就是从头开始x2嘛呜呜呜

[New frame: Personal Conversational Search](https://docs.google.com/document/d/1cqUDs-qgYWfci9rWkTFR32UqwCwS6Hps1eWOUFGZKa4/edit)

总之就是要变成找过去看过的东西的语音助手了？先从YouTube。邮件。和file三个小方向上实现，每个都有特定几个模块，在用户给出描述时进行匹配并引导用户进一步提问直到找到对应信息。

用mentor的话嗦，就是实现起来简单但是没人做过的东西，6鸭

现在的语音助手就实现不了x撒不垃圾的QAQ

---

晚上为了去concert特意四点半就肥来，结果被淋成一只全身湿哒哒的喵惹！窝枯了，为什么每次一有啥搬砖以外的活动就给窝下暴雨啊！来的时候也是粗去次饭也是fallingwater也是concert也是？？？

洗完澡次晚饭已经快8点了居然还热火朝天x

还有魔性蹦迪？但是小盆友萌都太可爱了叭嘤嘤嘤

最后和Patricia去前面夸他们23333

## 8.3 - 4.1

![esijbR.png](https://s2.ax1x.com/2019/08/03/esijbR.png)

email：

url直接获取 √

title: subject / time: date √

topic: innertext / length: innertext的length √

visitCount: 计数（已经有visitTime，只要看visitTime个数就行，底层会写）

type: (received - to 自己) / (sent: from 自己) / (forwarded: subject start with 'Fwd:') √

*Nturns: 咋计算？RE开头？一个界面里会有所有记录

link: website? clicked: 点击/存过没？url 除了点击√

attachment: type / name / 点击过没？/url 除了点击√

contact: from name / address / frequency咋计算 除了frequency√

---

YouTube：

URL √, Topic 不用, 

Length, WatchedLength √

 VisitCount, Title, Time, √

WatchListAdded, Liked, √

Commented, √

Type (music, vlog, etc.)

Uploader Name √, Subscribed √, VisitCount

Character Name

## 8.4 - 4.2

YouTube：

利用jQuery的点击listener √

click save 都会重复n次

video和email新存储 √ update函数还有问题，改了半天xikai嗦是js的问题23333明天问Micheal叭x

## 8.5 - 4.3

mentor粗去一周x窝也不叽到窝该高兴还是桑心QAQ

周三之前第一个目标是把video email完成存储并且测试 

第二个目标就是看一下sentby 和share to这里 具体利用页面点击行为来判断 比如sentby 这种就是先做Gmail 里面点击的link 对点击的link上面的发件人记录 shareto也先做邮件的 比如发送的邮件里面的link记录发送给了谁

---

早上上了托福课然后被Patricia嫌弃了，的确一般般叭，就九个人上还想咋样

下午mentor终于发信息来了x然后和他嗦循环更新出错的问题他一句把loop放promise里试试神它喵就work了？？？为啥啊！窝枯了

然后叫窝看的sentby和shareto嗦要

> 比如我想判断一个url是不是user paste in email里面的 我们需要:
>
> 1. 看看用户发送的email里面有没有link -> 现在我们知道email里面有没有link 但是没有判断某个email是不是用户发送的
> 2. 用paste event listener看看这个link 有没有paste到这封邮件里面

窝：喵喵喵？这什么逻辑这么复杂

于是窝嗦直接看已发送的邮件里有没有link，然后根据emailtype update这个link的sent 或者share就行？

mentor嗦：right

？？？？

行叭就这么做叭，然后发现link和type不在同个地方。。于是又得找load SPD的函数从最底层开始找了半天。。。最后返回的promise看都看不懂，data找都找不到。。。问另一个小伙伴又咕咕咕。窝。。卑微.jpg

然后mentor又嗦要用axios简化xhr，窝看了个栗子感觉差不多啊，可是他嗦是Micheal安利的，可以用promise？那就剪呗，剪完push pull完发现天都变了？？？roi直接消失了？？？

随之消失的还有各种初始化。。。

问mentor嗦你加一下？？窝加了也都是undefined啊！

枯了。明天看叭，窝头好冷呜呜呜呜呜呜呜呜呜呜呜呜

## 8.6 - 4.4

艹这个破电脑又自己关机。。。然后再次打开这个文件就是三天之后了？也不记得是没写还是写了没存，枯了，窝要买小水果！

但是汇率蹭蹭蹭的就上了7窝能咋办嘤嘤嘤，现在买还不如中国官网便宜嘤

看聊天记录才记起来这一天发生了啥。。

早上和mentor聊为啥代码会变成这样，然后他火速integrate了别的把video留给了我

然后午觉睡到四点半。。。头昏脑涨呜呜呜，一起来就见他问咋样，窝只能肥刚醒什么事23333，然后把video整进去之后发现arrive没法进去了？

然后问Micheal他半夜发来嗦以前没用过还在研究23333

## 8.7 - 4.5

本来是继续写email的sentby和sharedto的发现content里抓url的在roiextraction里啊？已经消失了啊？然后就试试直接在gmailHandler里抓呗。

于是又发现了新的问题，inject这样inject了好多次，然后在具体邮件页面刷新然后回到inbox再进邮件的时候就可以，但是在inbox刷新然后进具体邮件就不行，和Micheal嗦了之后秒速改好，tqlQAQ

加了之后发现存储又出问题了23333

修了这里漏了那里真的是x

---

看waterfront的网站一个个店看过去，好想买lego的迈凯伦啊嘤嘤嘤，坐等升值也行啊

去CWS买鞋子！shopping果然是很治愈啊qvqqqqqqqq

回来买pizza的时候又突然地暴雨。。。幸好窝带了伞。。。

## 8.8 - 4.6

不知道为啥失眠。。。然后每天早上四五点准时醒一次。好难受呜呜呜

然后十一点左右又睡了。。。睡到两三点起来次chili

---

mentor问进度咋样，窝：arrive也没修存储也没修，卑微.jpg

然后mentor突然喵修arrive，直接移到函数外就行了？？我好菜啊x

---

然后又不叽到干啥了。。。emmmm

哦defaultPage还没ok

？？？把窝的roi删成啥样了啊呜呜呜呜呜呜呜，important size都没了？？？窝的爱啊呜呜呜

然后找bookmarks的api，第一下mdn的browser居然不资词chrome？行叭你chrome你骄傲，于是用了chrome的 [API](https://developer.chrome.com/extensions/bookmarks#method-search) 为啥还是给窝报undefined？？？喵喵喵？窝加了permission了啊？佛了

---

好颓废呜呜呜，又刷了知乎，这里面的人才真的是个个说话又好听啊呜呜呜

> 借我一场秋啊，可你说这已是冬天。

呜呜呜呜呜呜

## 8.9 - 4.7

把default写了。。。。bookmarks还是喵喵喵

## 8.10 - 4.8

把YouTube时间存的逻辑优化了

把bookmarks solve惹

叫窝看NTurns，比较了id回溯和直接看innertext分割，还是选择了后者，神它喵写正则的时候发现空格不一样？？？惊了，就这样叭x头秃

## 8.11 - 4.9

想吖想吖想scenario~

update失败居然是spd还没创建？为啥不判断一哈。。。

---

NLP咋处理鸭

首先用户给出的句子要落到information_target上

root：有动词时是动词  - 对应的obj是要找的主体 / 没动词时直接是n为主体 / 要求时root不重要但是形容时重要（怎么区分？）

root - prep介词 - pobj主对象

怎么找type？在不同结构里？

窝的方法：所有generalize，直接dependency tree走到底x

好处：关系明确，不会漏；坏：处理复杂

## 8.12 - 5.1

先抓target（循环？太不elegant惹叭？之后再看。。

- pobj: object of a preposition / dobj: direct object（多个：看除去prep能否链接回root）
- nsubj: nominal subject（多个：看entity/词性）（只有在what问句中）
- advmod WH- （只有在开头时是，为问句）
- ~~advmod+nsubj+回溯关系 （需不需要有？不需要，nsubj应该作为限定描述）~~ 
- root为noun
- 优先级：开头advmod > noun的root > dobj/pobj （> nsubj what可先判断）

---

主要问题：

- keyword/entity/time优先级？平面化就是有这种问题。。
- time是用tmod加附属还是直接用识别时间那个
- entity之外得处理形容词
- type是keyword的一部分吗？给定keyword能对应固定type吗？
- entity和dependency咋对应

---

description：

包括：entity，形容词，时间

分级：keyword > entity > adj. ?

---

写了target的伪代码和测试代码还是很有成就感23333

party也还行x虽然还是社恐，但好在自己就是个翻译，大家也还是很nice~

明天把expand和description写惹！冲鸭！

晚上mentor把窝的target搞进去惹x抢我commit嘤嘤嘤，还叫我第一下不要在里面加！口亨！

不过如果我加的确加不了searchBar。。。哼

然后又和窝争关系的问题。。。窝佛了，窝可能只是需要一个催我的，不需要管窝的。。。

## 8.13 - 5.2

ok新的一天从头开始好叭

结果一开始就gg。。看昨天的undefined是因为异步请求还没请求完就返回了。然后嗦 [async await](https://javascript.info/async-await) 试一下？发现await资词是资词then的但是这写法我就不会了啊？

算了肥去看description叭。。

要求：不漏description、有准确关系（真的需要预设吗）、存储形式可对应match方式

另外还要考虑返回时语言生成。。。好复杂啊呜呜呜呜呜呜呜呜呜呜呜呜

呸。顶不住也得给窝顶。谁叫你这么懒。还这么菜！

---

target √

发现个bug，what开头也可能只有what为target。。。

回顾了一哈mentor的聊天记录感觉用语言传达想法太难了、、、qvq

---

expanded target - 应该把逻辑加在target里，优先级最高 √

往前看（所有句型都得看）：

- nn noun direct修饰
- amod adj 普通形容词修饰 （另外处理吧？）

往后看（所有句型）

- of指向的(pobj?) = noun direct修饰？

问句：（再说吧。。。感觉可能得放description里判断）

- what + nusbj -> dobj
- what -> pobj (relationship)


---


description

entity

- 单个词（无空格）

  已经在expanded target里：不管

  nn/tmod/amod：不管

- 多个词（有空格）

  将最后一个词按单个词过滤一遍

单个词过滤剩下：找direct和关系（链接前一个verb？）

多个词通过过滤：直接留下（不能分，比如check-in guide），找关系



amod形容词

是和tmod一样扫一遍再找对应还是直接和找direct一样每次找？

这个应该看会不会有不是在名词前面的形容词 / 扫一遍会扫到已经在entity里的amod

~~前面情况栗子里没有但窝觉得很可能会在从句里有(find the video which is very helpful)~~ 这种情况的形容词是 acomp: adjectival complement？？？惊了

后面的目前只在check-in guide这个奇葩里粗线x

总结起来正好？amod和direct一样往前找，然后acomp扫一遍？爽歪歪？（待定）



time：tmod还是chrono(好像一样，那就tmod叭)

要加前面的限定词和形容词（吗）



keyword除了type都是动词吗，如果是动词就会出现在关系里



---

test：

佛了就不能写在文档里吗QAQ，截的图神它喵和写的栗子不一样x面向自己想要的栗子截图：）

What's the number of the room I just reserved for tomorrow's meeting?

I'm looking for the email link Jake sent this early morning.

I'm looking for the link my Airbnb host sent me this morning on the check-in guide.

Play the new song from my favourite Japanese artist.

---

真的是一有户外活动就暴雨。。。这个雷好鸡儿可啪啊！感觉就打在头顶！呜呜呜呜呜呜呜呜呜呜呜呜

然后就被鸽了：）明明雨都停了形势一片大好QAQ

然后电话和mentor争parser咋写。。。气气！气洗惹！

总之是悲伤的一个晚上呜呜呜

## 8.14  - 5.3

为了蹭车6:30就来了。。。然后library没开。。。卑微

说好的八点他快九点了才来，枣嗦我就直接碎了呜呜呜

辞卑x

---

最后还是窝给他讲窝的。。。从开始到返回都给你安排好叭

还在异想天开整那些description的分类，你分了有啥子用x

---

好的既然整个流程都整理好了剩下的就是马呗。。。前一天还说分类重要分类有用，窝按窝的马要大改要拖延要浪费时间！哼！好气啊！

---

加找amod（advmod）的函数，poss（pron）

---

记录一下上次用到的查找object方法省的又忘。。

```
let obj = arr.find(o => o.name === 'string 1');
```
窝日刚刚插座插上之后瞬间黑屏而且开不了机了！窝以为窝凉了！心脏都停跳了好嘛呜呜呜呜

---

逻辑清晰写的飞快。。。躺呜呜呜

但总觉得接下来的match才是tricky，窝真的没力气解释，因为窝只是一只喵QAQ

看看他写的窝的逻辑。哼

![mAYsnf.jpg](https://s2.ax1x.com/2019/08/15/mAYsnf.jpg)

晚上waterfront肥来又zoom，然后解释窝的逻辑解释半天。哼！哼！！！

最后match还是落到坠坠坠简单的js search上。。。真的太不优雅了。。。

## 8.15 - 5.4

好叭那就暴力search呗x

match流程：

（过滤type - ）先从得到的对象里挑出可search的词 - 把fulltext match得到的结果都加在一起 - 通过field和时间过滤出结果 - （ADJ解析过滤） - （二次full text search） - 根据结果的分配+target返回给用户目标或继续问问题 - 直到返回target

需要做的：

一开始的type确定的尝试函数typeDetector √ 是否可信？ 

- 不太可信，可能会有两个keyword，此时会match前面的 （如pdf in email为doc类型，但需要去email找）-> 解决：type可以多个 √

- show不能确定为video（如show me blabla） -> 已注释 √

- 增加能推测出type的特定动词 √ （待补充）

- 找到一个用超长正则在字符串找数组匹配的方法。。。但是还是不优雅感觉x。但是比循环稍微好点？

  ```js
  if( (new RegExp( '\\b' + array.join('\\b|\\b') + '\\b') ).test(string) ) {
    alert('match');
  }
  ```

如果确定了type，只在固定type内search叭？这样先type再search算优化吗。。还是反过来也一样？

算了反正都是暴力憋固定type了。。

什么是可search的词？

- ~~不能是type类词汇（往往不会出现在plain text里）（但是搜了也无伤大雅？如果快的话？）~~ 
- n: `expanded_target.split(' ')` / `expanded_entity.split(' ')` 
- adj?

search结果加在一起再构成一个SQL的结构进行下一步匹配是否可行。。

field anchorKeyword 如何对应 ~~（在有无type确定的情况下）~~ 不对，现在是第一轮搜索后结果里对应匹配，所以肯定有type了，那就按照type具体field区分anchor

~~写了半天还是感觉好僵硬吖，谁叽到用户会嗦啥奇怪的描述QAQ，想到那个作为测试程序猿的笑话哈哈哈哈哈嗝~~ 



时间过滤（应该也会需要范围类keyword，不能直接依赖库）

如何根据target返回结果

如何继续生成问题

- 一个找到结果集中最能区分的field的算法（怎么感觉有点ML）

用户继续说的话处理 - 将utteranceParser作为一个模块，根据每个句子不同情况进行不同process：

- 同时输入除主句之外的话：有代词处理默认为target -> 其他分析同主句 ~~会有新的object吗~~ 
- 窝们提供问句之后的返回：问句回答（+对问句回答主体的其他描述）-> 回答匹配提问中的field（问句为询问具体field时） / 确定问句提出假设（问句为提问具体描述是否正确时） + 其他描述分析方法可同主句

---

其实今天啥都没做QAQ。。。

一直在网购。。。然后晚上又去惹Aldi shopping。。。

洗完澡再肥他叭（瘫

## 8.16 - 5.5

导师又走了，，，是真的所有工作都落在窝shoulder上啊，，而且你自己马还不行，还得给他们解释。。。窝好难x

今日TODO：

第一步：暴力js search！

searchWords提取 √

第二步：field match！

就这两步，看起来真它喵简单。。

然后就gg了：）react class还不能读state了？这么傲娇？？？一个要异步不能普通await一个要逻辑都写在你寄几肚子里？佛了。。。

把Parser移到searchBar里 √

模块化移回去。。 √

然后还是gg，this都undefined可还行，呜呜呜呜呜呜呜呜呜呜呜呜

prep好像找来找去也就几个，还是主要是动词叭这样看的话

直接用firebaseManager √

第一步 √

哦对时间还没解析。。QAQ

search多层的还是不ok吖，明天看叭QAQ

## 8.17 - 5.6

感觉马上就要走惹呜呜呜呜呜呜呜呜呜呜呜呜，有机会再来吗

cmu：有机？有机不会

呜呜呜呜呜呜呜呜呜呜呜呜呜呜汇率又涨学费又涨吃不起榨菜了好吗

---

改好了一层的转变函数 √

结构化searchWay √（为什么明明实现都没实现就追求偷懒和好看x

去重 √ （糕级啊！

originalDialog需要留存以便后续匹配，只是不加index √

神它喵窝之前的concat没用居然是因为它不直接改变数组而是返回新数组。。。窝好蠢x

加了typeClassify √

还以为forEach是什么好东西。。之前不能break，现在里面return都不能return的？

为什么又冒出来一个rcmod的动词啊。。。艹

感觉这个就只能是想啊想各种语言。。。

时间

动词anchor和field匹配

- loseMatch √

rank？去重的地方看看能不能加，还有match的地方

---

video目前资词：

from/about/liked/subscribed/commented/added

修改count返回

## 8.18 - 5.7

今日TODO：

除video外的存储结构更改和keyword

upper判断

时间

CONSUMER GOOD

三元符ide报错

default的最终匹配

---

唉mentor又催着想多句的和返回的了。。不过加了语音stt是真的糕级诶嘿嘿，除了不太准。。但是中文好准啊。。。难道是英语发音太烂QAQ

多句么就是上次想的搬过来：

> 用户继续说的话处理 - 将utteranceParser作为一个模块，根据每个句子不同情况进行不同process：
>
> - 同时输入除主句之外的话：有代词处理默认为target -> 其他分析同主句 ~~会有新的object吗~~ 
> - 窝们提供问句之后的返回：问句回答（+对问句回答主体的其他描述）-> 回答匹配提问中的field（问句为询问具体field时） / 确定问句提出假设（问句为提问具体描述是否正确时） + 其他描述分析方法可同主句

提供返回：

list中根据matchCount排序

有最高：搜target（target为type：返回url及对象；target为field：返回field value；target为内容：返回包含target这句话）

无最高：找到可区分field -> 生成问句

---

所以现在先想返回的问句和结果，这样可以和前端衔接起来嗯

那就是找个鉴别的算法呗

无最高：

if(!type && multiple types in result) What's the type of the information resource?

else if(same type in results) 还是得根据不同type看，每个type有一些可挑选为问句返回的fields

通用：

- ['visit_time']When did you visit it?
- ['VisitCount']have you visited it more than x times?
- ['Topic','Title']Is it about x?

video：

- ['WatchListAdded','Liked','Commented','Subscribed'] Have you xxx the video?
- ['UploaderName']Do you remember the uploader of the video?
- ['Length']Is it longer than x minutes?
- ['WatchedLength']Have you watched (more than half) of it?

email:

- ['AttachmentName']Does it have attachments?
- ['Type']Did you sent it or received it?
- ['ContactName']Who sent it to you? / Who did you send to?
- ['NTurns']Is it an email after x turns?

doc:

- ['Type']What's the type of the document?
- ['TimeSpent']Did you read it for a long time? (- product,webpage as well)
- ['Website']Does it contain any links? (- email as well)

product:

- ['CartAdded']Have you added it to your cart?
- ['Price']Is it more expensive than $x?
- ['ItemName']Do you want to find x or x?

webpage:

- ['Bookmarked','Commented']Have you x it?
- ['LastVisitTime']When did you visit it most recently?
- ['SharedToChannel','SentByChannel','SharedToName','SharedToTime','SentByName','SentByTime']Did you shared/received it (by x)/(to/from x)/(when)? (product,doc as well)

## 8.19 - 5.8

在匹村的倒数第二天qvq

十二点刚上床三点就被Sally一阵持续了几个小时的狂吠吵醒：）

刷了个空间发现AO3获hugo award惹！太牛逼了叭！疲惫生活的英雄梦想真的是呜呜呜啊

然后早上又是住家在good girl x n神它喵人类的本质

---

Micheal把前端整好了就又只剩窝马马马了。。唉振作！对自己马粗来的爱负责！

highest √

唉就这么点数据真的很难测试。。语音识别这准确度真的是醉了。。。

target加情况：第一个词是verb的句子 下面的dobj

target加情况：最后一个循环出不来到时

field先diff出来后的优先顺序直接是存储结构的先后吧，不然太麻烦惹qvq

---

虽然play被鸽了好歹还有个baseball game（虽然不太感冒

但还是人生或许仅有一次哒经历~体育馆的垃圾食品真的好好吃qvq

虽然匹村的棒球队太菜了最后0分x

虽然Micheal在边上给Hai解释窝还是不懂规则

但是downtown的河边还是很安详鸭~

从金华的湖边到西湖到武汉江边到那个有雾的湖边，有水的地方就有柴米油盐的生活和人烟~

十一点多回来知道睡不着随手把返回给写了

还是觉得emmmm

唉以后再优化把x

明天收拾！希望Amazon能靠谱点把包送到。。简直了

## 8.20 - 5.9

现在有的问题和todo：

field match方面

- 加field key `todo: add more keys` fieldHandler.js
- （每种type的match函数里）加upper判断 `todo: add upper logic here in every types' match function`  ，加default match `todo: add default fulltext match for other entities here` fieldHandler.js
- capital优化，现在是直接把首字母大写，但是field name是驼峰的。。 `todo: find another way to map words to field names` fieldHandler.js
- duplicate加count `todo: add count here` jsSearchHandler.js
- 时间match `todo: add time match logic here` fieldHandler.js
- 返回问句中field优先级
- 返回结果形式，现在只有url `todo: optimize return results` `todo: fulltext match` fieldHandler.js
- 格式化输出
- matchedList为空

解析方面：

- find target循环出不来
- 用户多句问题和答案对应和答案解析
- CONSUMER GOOD
- 第一个词是verb的句子 下面的dobj

其他：

- 新代码怎么有这么多response undefined
- 三元符ide报错（窝没有x
- 除了video的测试
- email update
- fuzzy match

用户回答分析：

（问题id在哪记录？）

无回答(don't remember / have no idea) 问下一个field问题

判断类 yes/no 直接找

描述类 对应问题field匹配

判断类+描述 -> 代词处理加nlp加match

## 8.21 - 6.0

于是就真的在机场和飞机上写总结惹QAQ

另外包果然没到，辣鸡x

TODO：

把TODO加到代码里 √

修改代码命名 (好像目前这几个文件里大致米有不规范的了鸭QAQ)

整理文档：todo+流程+问题栗子

写总结~

## 8.22 - 6.1

更新TODO：

field match方面

- 加field key `todo: add more keys` fieldHandler.js
- （每种type的match函数里）加upper判断 `todo: add upper logic here in every types' match function`  ，加default match `todo: add default fulltext match for other entities here` fieldHandler.js
- capital优化，现在是直接把首字母大写，但是field name是驼峰的。。 `todo: find another way to map words to field names` fieldHandler.js
- duplicate加count `todo: add count here` jsSearchHandler.js
- 时间match `todo: add time match logic here` fieldHandler.js
- 返回问句中field优先级 `todo: find priority instead of the first field` fieldHandler.js
- 返回结果形式，现在只有url `todo: optimize return results` `todo: fulltext match` fieldHandler.js
- 格式化输出 `todo: formatting output` backHandler.js
- matchedList为空 `todo: add count in loselist` fieldHandler.js

解析方面：

- find target循环出不来 `todo: fix the problem here` utteranceParser.js (栗子： `this is a bug`)
- 用户多句问题和答案对应和答案解析 backHandler.js
- CONSUMER GOOD `todo: add CONSUMER_GOOD to product type` utteranceParser.js
- 第一个词是verb的句子 下面的dobj `todo: add circumstance that start with verb: target is first dobj` utteranceParser.js

其他：

- ~~新代码怎么有这么多response undefined~~ 没了
- 三元符ide报错（窝没有x `todo: fix the error` jsSearchHandler.js
- 除了video的测试
- email update
- fuzzy match

用户回答分析：

（问题id在哪记录？）

无回答(don't remember / have no idea) 问下一个field问题

判断类 yes/no 直接找

描述类 对应问题field匹配

判断类+描述 -> 代词处理加nlp加match

---

总体流程大致：

![mr2wmF.png](https://s2.ax1x.com/2019/08/23/mr2wmF.png)

- 三角1：target获取逻辑（milestone有之前纸上写哒，附上自己码的时候写的早期版本。。后面有加的改动来着

![mrRsHg.png](https://s2.ax1x.com/2019/08/23/mrRsHg.png)

---

另外一些想到的：

- anchor动词应加入最后的fulltext匹配中，如where to pick up sb. 这种信息如果在email中，那target句子中必定需要pick来定位
- 加时间识别的时候在poss中也得扫一遍，upper为此时entity，如tomorrow's meeting，tomorrow为poss抓进了meeting这个description的poss数组中

------

最后希望deja wu这个项目可以早日发布~

四周的时间不长也不短，但刚刚好可以让你开始觉得你已经开始习惯这样的生活，刚刚好可以让你对这里有依恋和不舍，刚刚好是一个难忘夏日的长短吖~

Déjà Wù, find what you've seen.

![mspEDO.png](https://s2.ax1x.com/2019/08/23/mspEDO.png)

## 8.24

昨天写完整理。。。今天又开始马。。。我好卑微

就不能看看窝整理的吗就问问问。。。

加了video的topic

然后又叫我写deduplicate的count和list的回滚。。。窝真的好卑微

枯了

研究了半天dedup，最后发现是运算符优先级迷。。

佛了

todo：page topic句子里有其他type情况

## 8.25

神它喵他自己改了小写没改全让我fix。。。给您表演一个喵fix好叭

然后神它喵发现他原来一直不知道存储应该是一层的。。。上回窝commit的居然merge没了！现在还问uploader name咋不能命中。。。再给您喵fix好叭

又语音又语音 每次说的五分钟十分钟最后都是半小时一小时

窝真的太卑微了

然后就给他写discretize呗，还map。。。啥map啊

## 8.26

回校之后写了时间的匹配

- 第一下tmod抓的会漏


- chrono解析today，last week这种会只有start没有end

## 8.27

fix 时间：把chrono放进Parser过程 √

修改time match √

visit_time discretize 数组处理 √

title fulltext jssearch时打分权重不一样

[utterance错误合集](https://github.com/lxieyang/dejawu-dev/issues/82)

问题：

- login要点两次？
- Cannot read property 'responseString' of undefined -》 要清空


## 8.28

1. 分割不出最后一个dependency -》find最后的dependency √
2. upper仍旧在时间描述中 -》 加判断 √
3. ~~时间记录不匹配~~ 格式不一样，没问题
4. A.M.在句中会被googlenlp分为两句话 -》 nlp前replace √
5. today week 等无时间段 -》 增加end时间 √
6. 改了两次discrete time的数组？好像没冲突。。


## 8.29

。。命都是止痛药给的

---

本来说看jssearch参数和title打分的，但是他还在改这块所以继续看nlp。。。

看issue他提了个night的这种的确还得在time里加

然后今天看的是解析用户回答

先看看他重构的这都是些啥x

嗯总的来说还是很有条理的x不像我写的QAQ

嗯写facet的多句匹配呗

好坑啊。。。

多个key不同就不返回了？吓得窝以为窝改错了x

video的length怎么都存的不对的鸭 修好了 √

窝之前记的那个object的find方法居然是只能find到一个的？惊了，还是乖乖循环吧。。。

（应该没了，好难受呜呜呜x

想想就丢人，以后是不是得把药随身带着：）

## 8.30

唉又剁手。。窝为什么如此败家啊QAQ

---

type clarification √

response加matched形容

- jssearch每个word记录
- deduplicate更新
- 每个spd加matched word

videos输入返回多个spd

神它喵。。。fuck。。。什么迷惑行为啊。。。艹,spd同个field前后脚输出的居然和spd不对上？？？

## 8.31

哦窝叽到了。超冷漠.jpg

啥啊，为啥明明是不同word jssearch出来的结果list，在js看来依旧是同一个spd吗。。所以后来做的改变会直接影响到这个相同的spd。。。那还要什么deduplicate啊。。。枯了

终于记好了fulltext matchedword。。。头秃。一测发现为什么看有没有最高matchcount的逻辑在看有没有不同type之后啊。。。问了一哈嗦好像放前面也可以？？？明明是就应该放前面好吗。。。

---

然后发现多个dialog的spd这样变成旧的都还是存着了？然后第一反应是重新indexing，第二反应是每次terminal之后清空一下，最后是和导师语音描述了这个问题然后叫了Micheal外援233333，然后就一行deep copy解决原来的reference。tql

`      spd = JSON.parse(JSON.stringify(spd));`

其实道理窝都懂，就是窝不会js有啥办法，毕竟窝也是刚刚语音的时候才知道for循环除了in是取key的还有of可以直接取value？？？仿佛写了一暑假假的代码呜呜呜

---

于是就这样过去了一早上，还有任务有任务，窝玩新老婆都没时间呜呜呜

我好难

随便把calculateMatchScore给写了

## 9.1

唉又是新的桑桑的一天，花着本应该学TOEFL的时间调bug也不知道什么时候能有成果

昨天因为网的原因commit让他看说可以了，今天窝一试明明是不行的：）

而且video tracker为啥又有问题啊。。。html格式变了？

改好了新的uploadername获取

改了videotitle key

调了半天终于发现是他改的时候matchcount和matchscore混了：）我说怎么match半天没match上

返回result改成了type

## 9.2

.导师失联了该肿么办x

我好难。。。

先把response存了加上

为什么。。。神它喵。。。response逻辑又改成这副鬼样子了：）

阿弥陀佛。。。

善哉善哉。。。

find居然是用在对象数组里的。。。那对象的子对象咋找x

唉办法总是有的，只是el不elegant的区别x

明天如果还是失联就看email叭唉

## 9.6

唉鸭

一不注意又好几天忘了写。。

前几天大概就是又修了几个bug然后把返回句子给做了（target不是固定pagetype而是在内容中的情况）

然后就是把日了喵的成绩单终于打好了

---

email又粗线了bug

换了个函数又得重新获取：）

还有个正则匹配的问题。。。











