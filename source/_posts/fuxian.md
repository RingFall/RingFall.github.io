---
title: 复现ING~
date: 2018-04-07 23:09:36
categories: Blog
thumbnail: "https://s1.ax1x.com/2018/04/07/CPBqxg.jpg"
---

~~学长做哒的复现平台~为了养成记博客的好习惯，恩，挖个坑。~~

嗦起博客。。。想起来上次看到的——

> ###### 单身程序狗解决了一个技术难题后没有妹子可以炫耀或夸一下自己怎么办？
>
> 技术难题不一定是学科或工程方面的，可以就是自己在开发中遇到的一个问题，下了一番功夫之后终于解决了，那种酸爽的心情
> 有妹子的程序员就可以让妹子夸夸自己，自己在家熬夜的单身狗怎么办……
>
> 答：现在你明白了吧，为什么那么多程序员要写技术博客。
>
> From [知乎](https://www.zhihu.com/question/28987904/answer/42805814?utm_source=com.tencent.tim&utm_medium=social)

哈哈哈哈哈哈哈哈哈哈哈哈嗝，真的是贼几吧心酸啊，分分钟召唤粗蠢使来当窝的程序猿鼓励师2333333

总之，

[![CuHsSJ.md.jpg](https://s1.ax1x.com/2018/04/19/CuHsSJ.md.jpg)](https://imgchr.com/i/CuHsSJ)

### unser

不叽到为啥总觉得所有php反序列化都挺简单的==不过只要是做到过然后会了的那种web题都觉得简单吧==不会的就gg==目前见到的就两种

- 当序列化字符串中对象数大于真实对象数时绕过__wakeup()函数
- 因为处理序列的机制不同引起不同解释的反序列化漏洞

### pwnhub_sql

原题pwnhub的目瞪狗呆

[方方土超详细的wp](https://www.anquanke.com/post/id/104319)

- 笛卡尔积 heavyquery 来延时

   `select count(*) from information_schema.columns, information_schema.columns T1, information_schema.columns T2, information_schema.columns T3`

- 出题思路 get_lock('key',time)

  > get_lock()是Mysql的锁机制
  > (1)get_lock会按照key来加锁，别的客户端再以同样的key加锁时就加不了了，处于等待状态。
  > (2)当调用release_lock来释放上面加的锁或客户端断线了，上面的锁才会释放，其它的客户端才能进来。


  > mysql_connect() 脚本一结束，到服务器的连接就被关闭
  > mysql_pconnect() 打开一个到 MySQL 服务器的持久连接

  > 第一次加锁后，需要等待1~2分钟，让服务器将我们下一次的查询当做客户B

时间盲注总结：sleep()|benchmark()|heavy query|get_lock()|rlike

***

5-24更新，以后复现啥的都po这儿叭qvq

### 0ctf-ezDoor

找到一个有dockerfile的题！立马复现一波来用一用docker~

下载 `git clone https://github.com/LyleMi/My-CTF-Challenges.git` 

在dokerfile目录下 `sudo docker build -t 0ctf-ezdoor .`

然后。。。step1就停下来惹2333，报错 `Tag 7.0-apache not found in repository docker.io/library/php`

第一下以为是网速或者fq的问题，然鹅咋搞都不行，于是去阿里云找了个php7+Apache的源 `sudo docker pull registry.cn-hangzhou.aliyuncs.com/lxepoo/apache-php7`

然后把dockerfile第一行改成 `FROM registry.cn-hangzhou.aliyuncs.com/lxepoo/apache-php7 ` 虽然是窝按理解瞎猜的骚操作，结果对了23333

这儿还顺便学习了一波vi：

- 「ESC」命令行模式（移动光标|dd删除行|x删除字|:wq保存退出）
- 「i」插入模式（写）

然后build*2。。。又弹出一行红的。。白的唰唰唰地刷屏就很爽，突然冒出红的感觉要吓出心脏病QAQ `debconf: delaying package configuration, since apt-utils is not installed` 

百度回答：

> apt-utils包含了Ubuntu 16.04 LTS 的发布后的一些新命令，比如apt（Advanced Package Tool），它可以取代 apt-get、apt-cache 等功能。
>
> 这里我们用apt-get，可以忽略这个提示，不会影响。

期间无数次好久没反应，紧张的我吓得要心脏骤停。。。每次哒环境都能神经衰落（河鳝的微笑

报错*2 `chown: cannot access '/var/www/html/sandbox': No such file or directory`

米有就建一个呗 `RUN mkdir /var/www/html/sandbox/`

然后报错*3（哭 `AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2. Set the 'ServerName' directive globally to suppress this message`

看意思貌似问题不大，不慌23333，毕竟已经Successfully built惹~

`sudo docker run -dit -p 8585:80 --name 0ctf-ezdoor 0ctf-ezdoor`

然后因为窝用的是虚拟机，ifconfig一发看看ip，然后在本机访问ip:8585就可以访问啦~第一次用docker复现西气哎糊题，鸡冻嘿嘿嘿嘿嘿嘿

然后开始做~

首页就给出了源码：

```
<?php

error_reporting(0);

$dir = 'sandbox/' . sha1($_SERVER['REMOTE_ADDR']) . '/';
if(!file_exists($dir)){
  mkdir($dir);
}
if(!file_exists($dir . "index.php")){
  touch($dir . "index.php");
}

function clear($dir)
{
  if(!is_dir($dir)){
    unlink($dir);
    return;
  }
  foreach (scandir($dir) as $file) {
    if (in_array($file, [".", ".."])) {
      continue;
    }
    unlink($dir . $file);
  }
  rmdir($dir);
}

switch ($_GET["action"] ?? "") {
  case 'pwd':
    echo $dir;
    break;
  case 'phpinfo':
    echo file_get_contents("phpinfo.txt");
    break;
  case 'reset':
    clear($dir);
    break;
  case 'time':
    echo time();
    break;
  case 'upload':
    if (!isset($_GET["name"]) || !isset($_FILES['file'])) {
      break;
    }

    if ($_FILES['file']['size'] > 100000) {
      clear($dir);
      break;
    }

    $name = $dir . $_GET["name"];
    if (preg_match("/[^a-zA-Z0-9.\/]/", $name) ||
      stristr(pathinfo($name)["extension"], "h")) {
      break;
    }
    move_uploaded_file($_FILES['file']['tmp_name'], $name);
    $size = 0;
    foreach (scandir($dir) as $file) {
      if (in_array($file, [".", ".."])) {
        continue;
      }
      $size += filesize($dir . $file);
    }
    if ($size > 100000) {
      clear($dir);
    }
    break;
  case 'shell':
    ini_set("open_basedir", "/var/www/html/$dir:/var/www/html/flag");
    include $dir . "index.php";
    break;
  default:
    highlight_file(__FILE__);
    break;
}
```

好像不是很复杂的样叽，有以下几个action功能：

- pwd所在目录
- phpinfo信息
- reset重置ip文件夹
- time打印时间
- upload上传（后缀不可包含h）
- shell包含文件夹下index.php

然后。。从PHPinfo入手注意到 `opcache.enable => On => On` 这是啥呢，是php的缓存，于是思路就很明显了，利用缓存文件覆盖来传shell，这儿有很详细的文章和工具了 http://gosecure.net/2016/04/27/binary-webshell-through-opcache-in-php-7/ 中文版 http://drops.xmd5.com/static/drops/web-15450.html 后面也有file_cache_only禁止和validate_timestamp开启的bypass情况解析

首先找到上传缓存目录 `/tmp/cache/[system_id]/var/www/html/sandbox/[ip_remote_addr]/index.php.bin`

然后通过工具测出system_id和时间戳

用同样配置生成我们需要的bin缓存文件并把前两个参数写进去

构造表单上传后即可包含，使用没被禁用的函数获取flag，然后貌似就是逆向的事了x

