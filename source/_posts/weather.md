---
title: weather
date: 2019-05-14 22:24:46
tags:
thumbnail: "https://s2.ax1x.com/2019/04/29/El6CQK.png"
---

> 清江社雨初晴，秋香吹彻高堂晓。天然带得，酒星风骨，诗囊才调。沔水春深，屏山月淡，吟鞭俱到。算一生绕遍，瑶阶玉树，如君样、人间少。
>
> 未放鹤归华表。伴仙翁、依然天杪。知他费几，雁边红粒，马边青草。待得清夷，彩衣花绶，哄堂一笑。且和平心事，等闲博个，千秋不老。<p align="right">——吴泳 《水龙吟·寿李长孺》</p>

咳咳，讲正事之前。

马鸭窝文豪野犬真的太帅了！！！横滨第一歌姬中也大小姐的歌也超好听！！！网易云音乐已经有惹！！！战歌起啊！！！还看了舞台剧我的天哒宰真的太帅了，最后那个双黑窝可以！！！中也鞠躬最高！！！镜花酱第一下数数的效果真的是，虐洗惹呜呜呜！然后就是樋口太好看惹8！为什么是芥芥哒痴汉鸭！乱步桑也可爱洗窝惹（躺

还看惹文豪野犬~汪哒漫画！我的天，官方教你做人好吗嘤嘤嘤，心疼一秒我家chuye超~级傲娇又好心哒用哪个名字最长的异能帮老奶奶提袋叽hhhhh最后发现是哒宰！xswl23333333333还有还有官方双黑女装~awsl~

还有凹凸。。。窝惊了，这么个汝甚短的为什么最近几集都把我看哭了啊！~~凹凸脏话~~ 

然后就系窝可以吹烟雨唱杨州和山鬼辣！嘻嘻嘻，水龙吟指日可待~

还有一个就是智慧城市为什么只有十周课，因为它有好多实验qvq，无人机还是挺有意思~然后画地图也超有意思哒~窝性冷淡的完美配色真的太好看了嘿嘿嘿x

然后最近不知道为啥有种要是窝有一个运动手表就会爱上运动的错觉？明明不动才是坠好的运动QAQ然后游泳课因为这个不靠谱的游泳馆没了55555，窝哭爆，还变成了马拉松，，，

另外，今天去计院，某兰xx的态度真的是令我惊奇，你以为要不是签字我愿意来你这办公室吗？？？你自己根本就没有任何通知怪窝咯？？？之前骗我坑我你自己还它喵理所当然？？？每次来都能找到原因骂一顿？？？院长不在也骂窝？？？窝？？？（但还是要保持微笑。呵呵。是不是每个院都有这种xx老师啊。窝真的是惊了。阿弥陀佛。

好的昨天窝以为他只是偶尔这样今天发现学弟去也被骂了：）mmp

好的应该没啥废话了，下面是为了可以不去上屁眼通红课做的第一个小作业~爬取天气数据存入数据库然后可视化~

***

## 题目

> Made By RingFa1l_08163337

> E. 利用爬虫采集天气信息（4人）
>
> 天气数据存到数据库里；
>
> 数据可视化分析统计：各省会当日高低温、与去年同期比较、多日高低温预报、天气警报等（不必全做出来）。

> 项目/作业报告：题目，设计思路，开发环境配置，运行使用方法，运行效果截图，运行效果分析总结——缺陷、改进方法；
>
> 源代码；数据（数据库、文件、图片等形式）；可执行程序（可选）。 

### 开发环境配置

- Python 3.6.1
- SQLite 3.28.0
- beautifulsoup4 4.6.0
- requests 2.19.1

### 设计思路

#### 1.爬取数据存入数据库

- 使用requests库获取页面
- 使用BeautifulSoup库解析html
- 使用weather.db存储数据

####  2.数据可视化分析统计

- 使用pyecharts库画图

#### 七天预报功能

数据来源：www.weather.com.cn （有个坑是今天的天气在早上是高温/低温，晚上就只有一个温度了x

通过观察发现查询的网站城市对应url中的九位编码，获取对应关系存储在json文件中，编写根据城市查询对应编码的函数：

```python
def city2code(city_name):
	with open('city_code.json', 'r') as f:
		data = json.load(f)
	f.close()
	try:
		return data[city_name]
	except:
		sys.exit('no city {} information'.format(city_name))
```

用户输入城市，通过city2code函数得到编码，爬取生成url返回的html，使用BeautifulSoup结构化解析出七天预报的日期、天气状况、高低温、风向和强度信息：

```python
city = input("city:")
city_code = city2code(city)
url = "http://www.weather.com.cn/weather/{}.shtml".format(city_code)
res = requests.get(url)
res.encoding = 'utf-8'
bs = BeautifulSoup(res.text,"html.parser")
date = bs.select("li.sky > h1")
desc = bs.select("li.sky > p.wea")
temp = bs.select("li.sky > p.tem")
dir = bs.select("li > p.win > em")
level = bs.select("li > p.win > i")

result = []
for i in range(date.__len__()):
    date1 = date[i].text
    desc1 = desc[i].text
    temp1 = temp[i].stripped_strings
    temp1 = "".join(temp1)
    dir1 = dir[i]
    dir2 = dir1.select("span")
    if len(dir2) == 1:
        direction = "无持续风向"
    else:
        direction = dir2[0].get("title")+"-"+dir2[1].get("title")
    level1 = level[i].text
    result.append([city,date1,desc1,temp1,direction,level1])
```

连接数据库，先搜索原有表单中这个城市的信息并删除，如果没有week_weather表先建立，然后将新的数据存入后关闭连接：

```python
conn = sqlite3.connect('weather.db')
cursor = conn.cursor()
try:
    cursor.execute("delete from week_weather where city='{}'".format(city))
    print("delete old data")
except:
    cursor.execute('''create table week_weather (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        city char(100),
        date char(100),
        desc char(100),
        temp char(100),
        direction char(100),
        level char(100)
        );''')
    print("create new table")
for result1 in result:
    print(result1)
    insertsql = "insert into week_weather (city,date,desc,temp,direction,level) VALUES ('%s','%s','%s','%s','%s','%s')"
    cursor.execute(insertsql % (result1[0],result1[1],result1[2],result1[3],result1[4],result1[5]))
 
conn.commit()
cursor.close()
conn.close()
```

可视化脚本连接数据库取出所需城市信息并把高低温文本解析成数字，如果本身信息不全则输出缺失退出运行：

```
x = []
y1 = []
y2 = []
try:
    for row in cursor:
        x.append(row[2])
        h = row[4].split('/')[0]
        if h.find('℃'):
            high = int(h.split('℃')[0])
        else:
            high = int(h)
        try:
            low = int(row[4].split('/')[1].split('℃')[0])
        except:
            low = high
        y1.append(high)
        y2.append(low)
except:
    sys.exit("高低温信息缺失")
```

柱状图绘制并保存在result目录中：

```
bar = Bar()
bar.add_xaxis(x)
bar.add_yaxis("最高温度", y1)
bar.add_yaxis("最低温度", y2)
bar.set_global_opts(title_opts=opts.TitleOpts(title="{}七日高低温预测".format(city), subtitle="made by Ringfa1l"))
bar.render("result/{}_pre.html".format(city))
```

#### 各省会实时温度功能

数据来源：tianqi.eastday.com

同样是url由城市对应的拼音和一个五位编码组成，首先建立省会字典：

```python
dic1 = ['河北省', '山西省', '辽宁省','吉林省', '黑龙江省', '江苏省', '浙江省', '安徽省', '福建省', '江西省', '山东省', '河南省', '广东省', '湖南省', '湖北省', '海南省', '四川省', '贵州省', '云南省', '陕西省', '甘肃省', '青海省', '台湾省', '内蒙古自治区', '广西壮族自治区', '西藏自治区', '宁夏回族自治区', '新疆维吾尔自治区']
dic2 = ['石家庄', '太原', '沈阳', '长春', '哈尔滨', '南京', '杭州', '合肥', '福州', '南昌', '济南', '郑州', '广州', '长沙', '武汉', '海口', '成都', '贵阳', '昆明', '西安', '兰州', '西宁', '台北', '呼和浩特', '南宁', '拉萨', '银川', '乌鲁木齐']
dic3 = ['53698', '53772', '54342', '54161', '50953', '58238', '58457', '58321', '58847', '58606', '54823', '57083', '59287', '57687', '57494', '59758', '56294', '57816', '56778', '57036', '52889', '52866', '71294', '53463', '59431', '55591', '53614','51463']
dic4 = ['shijiazhuang', 'taiyuan', 'shenyang', 'changchun', 'haerbin', 'nanjing', 'hangzhou', 'hefei', 'fuzhou', 'nanchang', 'jinan', 'zhengzhou', 'guangzhou', 'changsha', 'wuhan', 'haikou', 'chengdu', 'guiyang', 'kunming', 'xian', 'lanzhou', 'xining', 'taibei', 'huhehaote', 'nanning', 'lasa', 'yinchuan', 'wulumuqi']
```

爬取数据：

```python
result = []
for i in range(dic1.__len__()):
    url = 'http://tianqi.eastday.com/{}/{}.html'.format(dic4[i],dic3[i])
    res = requests.get(url)
    bs = BeautifulSoup(res.text,"html.parser")
    data = bs.select("div.tempBox > span")
    temp = int(data[0].text)
    result.append([dic1[i],dic2[i],temp])
```

存入数据库live_weather表：

```python
conn = sqlite3.connect('weather.db')
cursor = conn.cursor()
try:
    cursor.execute("drop table live_weather;")
    print("delete old data")
except:
    pass
cursor.execute('''create table live_weather (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    province char(100),
    city char(100),
    temp int
    );''')
print("create new table")
for result1 in result:
    print(result1)
    insertsql = "insert into live_weather (province,city,temp) VALUES ('%s','%s','%d')"
    cursor.execute(insertsql % (result1[0],result1[1],result1[2]))
```

取出数据：

```python
conn = sqlite3.connect('weather.db')
c = conn.cursor()
print("opened database successfully")

try:
    cursor = c.execute("SELECT * from live_weather")
    print("data selected successfully")
except:
    sys.exit("No information")

city = []
temp = []
for row in cursor:
    city.append(row[2])
    temp.append(row[3])
```

画地图：

```python
def geo_base() -> Geo:
    c = (
        Geo()
        .add_schema(maptype="china")
        .add("省会温度", [list(z) for z in zip(city, temp)])
        .set_series_opts(label_opts=opts.LabelOpts(is_show=False))
        .set_global_opts(
            visualmap_opts=opts.VisualMapOpts(max_=30),
            title_opts=opts.TitleOpts(title="省会城市实时温度", subtitle="made by Ringfa1l"),
        )
    )
    return c

geo_base().render("result/live_temp.html")
```

#### 历史数据比较功能

数据来源：tianqi.eastday.com

使用time库获取当前年月日信息：

```python
year = str(int(time.strftime("%Y", time.localtime()))-1)
mon = time.strftime("%m", time.localtime())
day = time.strftime("%d", time.localtime())
```

循环爬取信息（这个网站有两种格式。。。所以加个判断~：

```python
result = []
for i in range(dic1.__len__()):
    for j in range(1,13):
        monn = int(mon)+j
        if monn > 12:
            monn = monn-12
            yearr = int(year) + 1
        else:
            yearr = int(year)
        url = 'http://tianqi.eastday.com/{}_history/{}_{}{:0>2d}.html'.format(dic4[i],dic3[i],yearr,monn)
        #print(url)
        res = requests.get(url)
        bs = BeautifulSoup(res.text,"html.parser")
        if bs.find_all(class_="item-value") != []:
            data = bs.find_all(class_="item-value")
            high = re.findall(r"\d+",data[0].text)
            low = re.findall(r"\d+",data[1].text)
            #print(high,low)
            try:
                result.append([dic2[i],yearr,monn,int(high[0]),int(low[0])])
            except:
                print(dic2[i]+'-'+str(yearr)+'-'+str(monn)+"data lost")
        else:
            data = bs.select("ul.history2_left > li")
            high = re.findall(r"\d+",data[0].text)
            low = re.findall(r"\d+",data[1].text)
            #print(high,low)
            try:
                result.append([dic2[i],yearr,monn,int(high[0]),int(low[0])])
            except:
                print(dic2[i]+'-'+str(yearr)+'-'+str(monn)+"data lost")
```

传入数据库his_weather表：

```python
conn = sqlite3.connect('weather.db')
cursor = conn.cursor()
try:
    cursor.execute("drop table his_weather;")
    print("delete old data")
except:
    pass
cursor.execute('''create table his_weather (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    city char(100),
    mon char(100),
    high int,
    low int
    );''')
print("create new table")
for result1 in result:
    print(result1)
    insertsql = "insert into his_weather (city,mon,high,low) VALUES ('%s','%s','%d','%d')"
    cursor.execute(insertsql % (result1[0],str(result1[1])+'年'+str(result1[2])+'月',result1[3],result1[4]))
```

获取特定城市数据：

```python
city = input("请输入一个省会城市:")

conn = sqlite3.connect('weather.db')
c = conn.cursor()
print("opened database successfully")

try:
    cursor = c.execute("SELECT * from his_weather where city='{}'".format(city))
    print("data selected successfully")
except:
    sys.exit("No information about {}".format(city))

time = []
high = []
low = []

for row in cursor:
    time.append(row[2])
    high.append(row[3])
    low.append(row[4])
```

画折线图：

```python
def line_base() -> Line:
    c = (
        Line()
        .add_xaxis(time)
        .add_yaxis("月平均最高温度", high)
        .add_yaxis("月平均最低温度", low)
        .set_global_opts(title_opts=opts.TitleOpts(title="{}历史气温比较".format(city), subtitle="made by Ringfa1l"))
    )
    return c

line_base().render("result/{}_his_compare.html".format(city))
```

### 运行使用方法和截图

- 先在目录下新建weather.db数据库

- 运行predict_7.py，按提示输入城市，输入错误会提示

  [![EH9YsH.md.png](https://s2.ax1x.com/2019/05/16/EH9YsH.md.png)](https://imgchr.com/i/EH9YsH)

- 运行predict_7_draw.py，按提示输入城市，画出的柱形图在result目录下

  [![EH9UeA.md.png](https://s2.ax1x.com/2019/05/16/EH9UeA.md.png)](https://imgchr.com/i/EH9UeA)

- 运行live_temp.py

  [![EH94YV.md.png](https://s2.ax1x.com/2019/05/16/EH94YV.md.png)](https://imgchr.com/i/EH94YV)

- 运行live_temp_draw.py，画出地图，html格式时移动鼠标可显示省市信息和具体温度值

  [![EH9OT1.md.png](https://s2.ax1x.com/2019/05/16/EH9OT1.md.png)](https://imgchr.com/i/EH9OT1)

- 运行history.py，输入省会城市

  ![EHFim4.png](https://s2.ax1x.com/2019/05/16/EHFim4.png)

  ![EHkn5n.png](https://s2.ax1x.com/2019/05/16/EHkn5n.png)

- 运行history_draw.py，画出历史比较折线图

  [![EHk3KU.md.png](https://s2.ax1x.com/2019/05/16/EHk3KU.md.png)](https://imgchr.com/i/EHk3KU)

### 运行效果分析总结

|       脚本        |    缺陷     |       解决方法       |
| :-------------: | :-------: | :--------------: |
|  predict_7.py   |  用户输入不可信  |  加入是否是可查询城市的判断   |
| history_draw.py | 输入不是省会城市  | 加入数据库中是否有相关信息的判断 |
|   history.py    | 网站提供两种格式  |   分别进行不同的解析程序    |
|        *        |  网站数据缺失   |    加入判断并给用户提示    |
|        *        | 可视化结果难以区分 |   通过格式化创建特定文件名   |

悄咪咪寄几的总结：tcl，这么简单的破脚本写了好几天QAQ，pyecharts好好看鸭

更新：用pyinstaller转exe果然处处是坑嘤。

更新+1：zcz什么屁屁态度！窝做的这么好看！性冷淡画风！还集成，集成个屁屁，徒儿嗦的果然没错x

***

好8后面依旧是吐槽

因为根本没有认真地投实习所以直到现在才收到了第一个电话面试qvq总结一哈记得的（我这记性应该漏了好多。。

- java站，框架
- 挖过的洞
- 内网渗透
- 软件，kali，smf
- 注入，gbk
- xxe，无回显，防护
- 经历，比赛，夏令营
- 平常看啥
- re，pwn
- 有米有欧否，8月入职太晚，考研看法，预期薪资

然后是另一个面试。。。为了这个去住了宾馆，结果神它喵是个不可描述的宾馆。。。艹。然后用Skype真的好糕级鸭！视频的时候背景模糊真的超棒（叫窝爸妈赶紧装上以后这样视频嘻嘻），还有录屏还有字幕！然后。坑的。就是。它瞧不起窝几十块的耳机嘛！一定要窝用索尼大法老婆才给麦克风声音？？？窝它喵又从宾馆肥寝室拿。。。

- 简单介绍自己，经历规划
- 安全方面做的题，我负责的方向
- 会不会js，前端开发经历
- 为什么想转hci
- 他介绍他的两个项目（一个是预测下一句一个是直接搜索给回答
- 窝就项目的提问和窝能担任的部分

中途电脑死机了一次，外面还很吵。。。早知道是音频面试就直接在寝室阳台面了QAQ，这破宾馆晚上还睡不着。第二天早上还环测学院的实验啊！

然后过惹。虽然8既然适合就是没啥悬念的。虽然这意味着窝要破产了QAQ。蛋窝为什么还挺开心啊扣唉扣5555

***

>汚れつちまつた悲しみに
>
>今日も小雪の降りかかる
>
>汚れっちまった悲しみに
>
>今日も风さえ吹きすぎる
>
>汚れっちまった悲しみは
>
>たとえば狐の革裘
>
>汚れっちまった悲しみは
>
>小雪のかかってちぢこまる
>
>汚れっちまった悲しみは
>
>なにのぞむなくねがうなく
>
>汚れっちまった悲しみは
>
>懈怠のうちに死を梦む
>
>汚れっちまった悲しみに
>
>いたいたしくも怖気づき
>
>汚れっちまった悲しみに
>
>なすところもなく日は暮れる
>
><p align="right">中原中也《汚れつちまつた悲しみに...》</p>

