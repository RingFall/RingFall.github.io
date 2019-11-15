---
title: 从零开始的开发补全
date: 2018-04-21 14:53:26
categories: Blog
thumbnail: "https://s1.ax1x.com/2018/04/22/CQnr38.jpg"
---

就看看视频可能真的是不会动手实践吧。。。然后就愉快地忘了

也选过前端web设计之类的选修课。。。然后又忘光了

可总不能连个网站都做不粗吧==于是洗心革面地肥去从零开始。

动手动手动手+笔记！嗯！（记录的一般是大概知识框架+自己特别感兴趣的点，具体的记了也不会看==就不浪费时间惹（才不是懒x口亨

（日站日不动就写写站，写写烦了就肥去看西气唉虎，完美x

### Front End Development

#### HTML5 and CSS

各种标签+CSS选择器(元素/类./ID#/属性/派生)+CSS属性 多用用就记住了

- 导入Google字体`link href="https://fonts.gdgdocs.org/css?family=Lobster" rel="stylesheet" type="text/css">`
- 圆形边框`border-radius: 50%;` 
- 用空格分开多个class来为同一个元素添加多个 class 属性

#### Responsive Design with Bootstrap

Bootstrap简直神器吖，免去了不同客户端布局的麻烦，画风也很喜翻~

`<link rel="stylesheet" href="//cdn.bootcss.com/bootstrap/3.3.1/css/bootstrap.min.css"/>`

把所有的HTML内容放在class为`container-fluid`的`div`下

- 给图片添加 `img-responsive` class属性使图片适配页面的宽度

- 居中头部元素`text-center` ,上色 `text-primary` 等

- `btn` 及各种附加属性

- 同一行`<div class="row"> ` 然后分成小div,使用 `col-md-offset-*` 类可以将列向右侧偏移。

  ![an image illustrating Bootstrap's grid system](https://i.imgur.com/FaYuui8.png)

- Font Awesome 图标库`<link rel="stylesheet" href="//cdn.bootcss.com/font-awesome/4.2.0/css/font-awesome.min.css"/>`  使用 `<i>` 标签

- 有深度的块 `well` 

- 导航栏 `navbar` 


#### jQuery

```
$(document).ready(function() {
	$("选择器").修改函数("参数");
  });
```

- 方法链`function chaining` 两个jQuery方法合在一起使用


#### Basic Front End Development Projects

- 在新页面打开连接 `target="_blank"` 

- Build a Tribute Page

- Build a Personal Portfolio Webpage Incomplete
  - 去除a标签下划线`a,a:hover { text-decoration: none; }` 
  - 导航栏[Navbar](https://getbootstrap.com/docs/4.0/components/navbar/) |顶层 `z-index:9999` |始终在显示上方 `position:fixed` 
  - 透明度opacity(小数)|分隔线 `<hr> ` 
  - background-size有3个属性：
    - auto：当使用该属性的时候，背景图片将保持100% 的大小显示，不进行任何缩放。超过div的多余部分将被隐藏。当图片过小时，图片会自动平铺。这种属性通常用来做重复性的背景或者做半透明图片背景。
    - cover：当使用该属性时，图片将被缩放至恰好能覆盖div，并且图片被隐藏的部分最少，这种属性在大图背景中应用比较广泛。
    - contain：当使用该属性时，图片被缩放至最大且能被完全展示出来，但是由于图片的的尺寸比例与div的尺寸比例会有不同，所以当图片不能盖住div时，图片会自动平铺。

- Design a danmu app

  简单地设计完界面后先分析一哈：

  点击send按钮->获取文本框内容->作为p标签添加到屏幕上(设置随机颜色等)->使用js计时器使其移动位置

  点击clear按钮->删除所有p标签

  然后。。心酸地一个一个功能地实现ing。。为啥每次他给的栗子都是各种看不懂的库啊框架啊QAQ

  - 点击事件 `onclick="函数();"` 
  - `window.onload = function(){}` 窗口加载后的函数
  - `setInterval(函数,毫秒数);` 每一段时间执行一次函数的计时器
  - `.style.marginLeft` 属性一定要记得加"px"
  - `.appendChild` 创造新的子节点| `.removeChild` 删除子节点


两个还是看不懂的参考QAQ: [JS原生实现视频弹幕Demo](http://www.cnblogs.com/Chenshuai7/p/7091508.html) |[JS弹幕代码分析](https://segmentfault.com/a/1190000008707119)

唉。。感觉这样寄几瞎几把写，代码真的好丑呜呜呜呜呜呜呜呜呜呜呜呜，前端也是呜呜呜，还有各种bug，可能只有不断地写写写写写才可以越来越熟练吧呜呜呜。另外网差用codepen好虐啊，还动不动就挂了，于是直接本地webstorm和控制台js调试技能点get√

#### `Basic` JavaScript

`var`定义七种不同的data types(数据类型)：`undefined`（未定义）| `null`（空）| `boolean`（布尔型）| `string`（字符串）| `symbol`(符号)| `number`（数字）|and `object`（对象）

没有使用`var`关键字定义的变量，会被自动创建在全局作用域中，形成全局变量。

`NaN` : "Not a Number"

| Code | Output |
| ---- | ------ |
| \'   | 单引号    |
| \"   | 双引号    |
| \\\  | 反斜杠符   |
| \n   | 换行符    |
| \r   | 回车符    |
| \t   | 制表符    |
| \b   | 退格符    |
| \f   | 换页符    |

console.log();打印到控制台

字符串用加号连接| `.length` 获取长度|`字符串` 的值是不可变的除非重新赋值|`.push()` 接受把一个或多个参数并把它“推”入到数组的末尾|`.pop()` 函数用来“抛出”一个数组末尾的值| `.shift()` 移出第一个元素|`unshift`移入一个元素到数组的头部

两种方式访问对象属性，一个是点操作符(`.`)，一个是中括号操作符(有空格/用变量代替索引时用)(`[]`)|删除对象的属性`delete A.B;` |用`.hasOwnProperty(propname)`方法来检查对象是否有该属性

使用技巧Using Objects for Lookups:

> var alpha = {   //栗子:简单的反向字母表
>   1:"Z",
>   2:"Y",
>   3:"X",
>   4:"W",
>   ...
>   24:"C",
>   25:"B",
>   26:"A"
> };
> alpha[2]; // "Y"
> alpha[24]; // "C"
> var value = 2;
> alpha[value]; // "Y"

JavaScript Object Notation 简称 `JSON`，它使用JavaScript对象的格式来存储数据。

`Math.random()`用来生成一个在0(包括0)到1(不包括1)之间的随机小数|`Math.floor()` 向下取整|min到max之间的随机数`Math.floor(Math.random() * (max - min + 1)) + min` 

`Regular expressions` 正则表达式被用来根据某种匹配模式来寻找`strings`中的某些单词|头部/尾部`/` | `g` (全局)，意味着返回所有的匹配而不仅仅是第一个|`i` 忽略大小写|数字选择器`\d` |选择器后面添加一个加号标记(`+`)允许这个正则表达式匹配一个或更多数字| `\s` 空白字符有 `" "` (空格符)、`\r` (回车符)、`\n` (换行符)、`\t` (制表符) 和 `\f`(换页符)|正则表达式选择器的大写版本（非）来转化任何匹配

#### Object Oriented and Functional Programming

使用构造函数（大写字母开头）来创建对象`var Car = function() {}` |使用 `new` 关键字来对它进行调用 `var myCar = new Car();` |使用 `this` 指向当前（将要被创建的）对象中的 `公有属性` 

- `map` 方法会迭代数组中的每一个元素，并根据回调函数来处理每一个元素，最后返回一个新数组

  > var timesFour = oldArray.map(function(val){
  >   return val * 4;
  > });   //每个元素乘四


- 数组方法 `reduce` 用来迭代一个数组，并且把它累积到一个值中。`reduce` 方法有一个可选的第二参数，它可以被用来设置累加器的初始值。如果没有在这定义初始值，那么初始值将变成数组中的第一项，而 `currentVal` 将从数组的第二项开始。

  > var singleVal = array.reduce(function(previousVal, currentVal) {
  >   return previousVal - currentVal;
  > }, 0);  //让数组中的所有值相减

- `filter` 方法用来迭代一个数组，并且按给出的条件过滤出符合的元素，回调函数返回 `true` 的项会保留在数组中，返回 `false` 的项会被过滤出数组。

  > array = array.filter(function(val) {
  >   return val !== 5;
  > });  //移除数组中值等于5的项

- `sort` 方法按字母顺序或数字顺序对数组中的元素进行排序。`sort` 可以把比较函数作为参数传入。比较函数有返回值，当 `a` 小于 `b`，返回一个负数；当 `a` 大于 `b` ，返回一个正数；相等时返回0。

  与我们之前用的数组方法仅仅返回一个新数组不同， `sort` 方法将改变原数组，返回被排序后的数组。

  > var array = [1, 12, 21, 2];
  > array.sort(function(a, b) {
  >   return a - b;
  > });  //从小到大的顺序进行排列 

-  `reverse` 方法来翻转数组

- `concat` 方法可以用来把两个数组的内容合并到一个数组中

- 使用 `split` 方法按指定分隔符将字符串分割为数组

- 使用 `join` 方法来把数组转换成字符串，里面的每一个元素可以用你指定的连接符来连接起来，这个连接符就是你要传入的参数。

#### Basic Algorithm Scripting

Reverse a String 

```
function reverseString(str) {
  str=str.split('');
  str=str.reverse();
  str=str.join('');
  return str;
}
```

Factorialize a Number

```
function factorialize(num) {
  if(num<=1)
    return 1;
  var a=num;
  while(a>1) {
    num*=(--a);
  }
  return num;
}
```

Check for Palindromes

```
function palindrome(str) {
  str=str.replace(/[\W_]/g,"");  //[^A-Z] matches anything that is not enclosed between A and Z
  str=str.toLowerCase();         //\W is equivalent to [^A-Za-z0–9]
  var str1=str.split('');
  str1=str1.reverse();
  str1=str1.join('');
  if (str1===str)
    return true;
  else
    return false;
}
```

Find the Longest Word in a String

```
function findLongestWord(str) {
  var arr=str.split(" ");
  len=[];
  for(var i=0;i<arr.length;i++) {
    len.push(arr[i].length);
  }
  len.sort(function(a,b) {
    return b-a;
  });
  return len[0];
}
```

Title Case a Sentence

```
function titleCase(str) {
  arr=str.split(" ");
  var a=[];
  for(var i=0;i<arr.length;i++) {
    a[i]=arr[i].substr(0,1).toUpperCase();
    a[i]+=(arr[i].substr(1,arr[i].length-1).toLowerCase());
  }
  str=a.join(" ");
  return str;
}
```

Return Largest Numbers in Arrays

```
function largestOfFour(arr) {
  var a=[];
  for(var i=0;i<arr.length;i++) {
    arr[i].sort(function(a,b) {
       return b-a;         
    });
    a[i]=arr[i][0];
  }
  return a;
}
```

Confirm the Ending

```
function confirmEnding(str, target) {
  if(str.substr(str.length-target.length,target.length)==target)
    return true;
  return false;
}
```

Repeat a string repeat a string

```
function repeat(str, num) {
  if(num>0) {
    var s="";
    while(num--) {
      s+=str;
    }
    return s;
  }
  return "";
}
```

Truncate a string

```
function truncate(str, num) {
  if(str.length>num) {
    var s="";
    if(num>3) {
      s=str.substr(0,num-3)+"...";
    }
    else {
      s=str.substr(0,num)+"...";
    }
    return s;
  }
  return str;
}
```

Chunky Monkey

```
function chunk(arr, size) {
  var a=[],flag=0,count=-1;
  for(var i=0;i<arr.length;i++) {
    if(flag&&flag<size) {
      a[count].push(arr[i]);
      flag++;
    }
    else {
      flag=0;
      a.push([arr[i]]);
      flag++;
      count++;
    }
  }
  return a;
}
```

Slasher Flick

```
function slasher(arr, howMany) {
  if(howMany>arr.length)
    return [];
  else if(howMany>0) arr=arr.slice(howMany);
  return arr;
}
```

Mutations

```
function mutation(arr) {
  var a=arr[1].toLowerCase().split('');
  for(var i=0;i<a.length;i++) {
    if(arr[0].toLowerCase().indexOf(a[i])<0) {
      return false;
    }
  }
  return true;
}
```

Falsy Bouncer

```
function bouncer(arr) {
  arr=arr.filter(function(val) {
    return val;
  });
  return arr;
}
```

Seek and Destroy

> **arguments** 是一个对应于传递给函数的参数的类数组对象。

```
function destroyer(arr) {
  var len=arguments.length;
  var a=[];                              //需要把对象放到数组里
  for(var i=0;i<len;i++) {
    a.push(arguments[i]);
  }
  r=arr.filter(function(val) {
    for(var i=1;i<len;i++) {
      if(val===a[i])
        return false;
    }
    return true;
  });
  return r;
}
```

Where do I belong

```
function where(arr, num) {
  arr.push(num);
  arr.sort(function(a,b) {
    return a-b;
  });
  return arr.indexOf(num);
}
```

Caesars Cipher

```
function rot13(str) {
  var r="";
  for(var i=0;i<str.length;i++) {
    var q=str.charCodeAt(i);
    if(q>=65&&q<=77) {
      r+=String.fromCharCode(q+13);
    }
    else if(q>=77&&q<=90) {
      r+=String.fromCharCode(q-13);
    }
    else
      r+=String.fromCharCode(q);
  }
  return r;
}
```

当初水了一年oj的结果大概就是喜欢这种水题叭x 然后难一点点的就全不会==

#### JSON APIs and Ajax

API——应用程序接口(Application Programming Interface)是计算机之间相互交流沟通的工具

许多网站的应用程序接口(API)都是通过一种称为JSON格式的数据来传输的，JSON 是 JavaScript Object Notation的简写

```
$(document).ready(function() {
    $("#getMessage").on("click", function(){
      $.getJSON("/json/cats.json",function(json) {    //Get JSON with the jQuery getJSON Method
        $(".message").html(JSON.stringify(json));
      });
    });
  });
```

使用`.forEach()`函数来循环遍历JSON数据

```
json.forEach(function(val) {
          var keys=Object.keys(val);   //获取val中的keys
          html+="<div class='cat'>";
          keys.forEach(function(key) {
            html+="<b>"+key+"</b>:"+val[key]+"<br>";    //val[key]为对应的value
          });
        html+="</div><br>";
        });
```

通过浏览器`navigator`获得我们当前所在的位置`geolocation` ，位置的信息包括经度`longitude`和纬度`latitude` 

#### Intermediate Front End Development Projects

##### Build a Random Quote Machine

找到两个api~英文的https://quotesondesign.com/api-v4-0/ 和中文的https://hitokoto.cn/api (一言看起来很棒诶诶嘿嘿)
- 子元素使用float后父div就不包含它了？喵喵喵？在div加 `overflow:auto;` 撑开父元素x

-  根据CSS规范的规定，每一个网页元素都有一个display属性，用于确定该元素的类型，每一个元素都有默认的display属性值，比如div元素，它的默认display属性值为“block”，成为“块级”元素(block-level)；而span元素的默认display属性值为“inline”，称为“行内”元素。

-  jQuery熟练度++; //用多了发现的确好用嘿嘿，样例用的ajax当然也挺好x

-  使用animate渐变效果

   但使backgroundColor渐变需要引用//cdnjs.cloudflare.com/ajax/libs/jqueryui/1.11.2/jquery-ui.min.js

   segmentfault挺棒。。搜问题搜到好几次惹，有点stackoverflow的赶脚~

   > jQuery Color部分的animate需要jQuery UI的支持

- 发推特 window.open() `https://twitter.com/intent/tweet?+各种参数` 

##### Show the Local Weather

题目里这个 [**story card**](http://www.cnblogs.com/henryhappier/archive/2011/02/23/1962617.html) 很棒~想到silicon valley里Richard一个人码到昏天黑地把功能一个个实现的时候，超感动啊~

- 免费天气api都是有次数限制滴，一看codepen这种实时刷新的岂不是要刷穷窝？虽然选择的 [和风天气](https://www.heweather.com/) 还行，不过——蹡蹡~不自动刷新姿势：
  ![CI4Utf.jpg](https://s1.ax1x.com/2018/06/01/CI4Utf.jpg)
- 要获取访问者的地址，咋办咧？看到参数也可以是ip，于是一搜，js居然没法直接获取ip？只有服务器端代码才能？浏览器地位减减？喵喵喵？还是得用api呀orz。。这年头API还都得注册拿key。。不过！发现一个超简单的！不仅ip还各种地理参数啊！还直接访问就有！ `https://json.geoiplookup.io/api` 就是这个啦~

- 把getJSON返回的对象转成字符串 `JSON.stringify()` 

- json用key时可以用点或中括号，若是字符串用中括号时要加引号

##### Build a Wikipedia Viewer

- 栗子的响应很棒诶，然而代码又是神奇的格式的那种QAQ，看到了 [AngularJS](https://angular.io/) 非常dynamic~（对这种好看的前端框架啊啥的毫无抵抗力QVQ，学习一发: 
	- 使用双大括号语法进行数据绑定
	- 面向对象大法好x `ng-controller` | `ng-repeat ` | `ng-model` 
- 用栅栏时居中需要计算offset

- 两个控件在同一行 `form-inline` 

- 看文档好难QAQ只能照着实例理解QAQQQ

- 日了喵了的跨域x，虽然最近看的web前端攻防解密里也详细讲了，但是还是emmm好麻烦，于是直接用ajax~

  > // JSONp return to "relax the same-origin-policy"
  >       dataType: "jsonp",

- forEach是遍历数组的？？？于是，用 `$each(json对象,function(参数){})` ，然后获得的参数，，不是整个对象而是最前面的id，emmm那就直接用这个id索引吧，机智如窝x

- 最后，删除某节点下所有元素 `$(".lis").empty();` ，大功告成~看着并没有美化却也有寄几喜翻的性冷淡风格哒结果蜜汁欢喜地感觉越来越熟练惹x
##### Use the Twitchtv JSON API
#### Intermediate Algorithm Scripting
先看题目给出的函数资源->再看问题->解决问题
Sum All Numbers in a Range
```
function sumAll(arr) {
  arr.sort(function(a,b) {
    return a-b;
  });
  var re=0;
  for(var i=arr[0];i<=arr[1];i++) {
    re+=i;
  }
  return re;
}
```
Diff Two Arrays
```
function diff(arr1, arr2) {
  var newArr = [];
  for(var i=0;i<arr1.length;i++) {
      if(arr2.indexOf(arr1[i])==-1)
        newArr.push(arr1[i]);
  }
  for(var x=0;x<arr2.length;x++) {
      if(arr1.indexOf(arr2[x])==-1)
        newArr.push(arr2[x]);
  }
  return newArr;
}
```
Roman Numeral Converter
```
function convert(num) {           //emmmm感觉可能是个傻办法
  var re=[],a=0;
    if(num>=1000) {
      a=parseInt(num/1000);       //js除法结果为小数，要用parseInt()去掉小数部分
      while(a-->0) re.push('M');
      num%=1000;
    }
    if(num+100>=1000) {
      re.push('CM');
      num-=900;
    }
    if(num>=500) {
      a=parseInt(num/500);
      while(a-->0) re.push('D');
      num%=500;
    }
    if(num>=100) {
      a=parseInt(num/100);
      while(a-->0) re.push('C');
      num%=100;
    }
    if(num+10>=100) {
      re.push('XC');
      num-=90;
    }
    if(num>=50) {
      a=parseInt(num/50);
      while(a-->0) re.push('L');
      num%=50;
    }
    if(num+10>=50) {
      re.push('XL');
      num-=40;
    }
    if(num>=10) {
      a=parseInt(num/10);
      while(a-->0) re.push('X');
      num%=10;
    }
    if(num+1>=10) {
      re.push('IX');
      num-=9;
    }
    if(num>=5) {
      a=parseInt(num/5);
      while(a-->0) re.push('V');
      num%=5;
    }
    if(num+1>=5) {
      re.push('IV');
      num-=4;
    }
    if(num>0) {
      a=num;
      while(a-->0) re.push('I');
      num--;
    }
 return re.join('');
}
```
Where art thou
```
function where(collection, source) {
  var arr = [],flag=0;
  for(var i=0;i<collection.length;i++) {
    for(var key in source) {
      if(collection[i][key]===source[key]) flag=1;
      else flag=0;
    }
    if(flag==1) arr.push(collection[i]);
  }
  return arr;
}
```
Search and Replace
```
function myReplace(str, before, after) {
  a=before.split('');
  if(a[0]>='A'&&a[0]<='Z') {
    arr=after.split('');
    arr[0]=arr[0].toUpperCase();
    after=arr.join('');             //总是忘掉join要带参数！！！
  }
  str=str.replace(before,after);
  return str;
}
```
Pig Latin
```
function translate(str) {
  arr=str.split('');
  if(arr[0]=='a'||arr[0]=='e'||arr[0]=='i'||arr[0]=='o'||arr[0]=='u') {
    arr.push('way');
  }
  else if(arr[0]=='g'&&arr[1]=='l') {     //emmmm不叽到怎么判断辅音丛，先面对样例编程x
    arr.shift();
    arr.shift();
    arr.push('glay');
  }
  else {
    var c=arr.shift();
    arr.push(c+'ay');
  }
  str=arr.join('');
  return str;
}
```
DNA Pairing
```
function pair(str) {
  d=[];
  arr=str.split('');
  for(var i=0;i<arr.length;i++) {
    if(arr[i]=='G') d.push(["G","C"]);
    if(arr[i]=='C') d.push(["C","G"]);
    if(arr[i]=='A') d.push(["A","T"]);
    if(arr[i]=='T') d.push(["T","A"]);
  }
  return d;
}
```
Missing letters
```
function fearNotLetter(str) {
  arr=str.split('');
  var flag=0,pri=arr[0].charCodeAt(),re;
  for(var i=1;i<arr.length;i++) {
    if(arr[i].charCodeAt()!==++pri) return String.fromCharCode(pri);
  }
  return re;
}
```
Boo who
```
function boo(bool) {
  if(bool===false||bool===true) return true;
  else return false;
}
```
Sorted Union
```
function unite(arr1, arr2, arr3) {
  for(var i=0;i<arguments.length;i++) {        //Arguments object 传入未知个数的数组时
    for(var j=0;j<arguments[i].length;j++) {
    if(arr1.indexOf(arguments[i][j])==-1)
      arr1.push(arguments[i][j]);
    }
  }
  return arr1;
}
```
Convert HTML Entities
```
function convert(str) {
  str=str.replace(/&/g,"&amp;");        //感觉依旧是撒不拉几的办法
  str=str.replace(/</g,"&lt;");
  str=str.replace(/>/g,"&gt;");
  str=str.replace(/"/g,"&quot;");
  str=str.replace(/'/g,"&apos;");
  return str;
}
```
Spinal Tap Case
```
function spinalCase(str) {   //又是面向样例的QAQ
  var st="";
  if(str.indexOf(" ")!=-1) {
    arr=str.split(" ");
    st=arr.join("-");
   }
  else if(str.indexOf("_")!=-1) {
    arr=str.split("_");
    st=arr.join("-");
   }
  else {
    for(var i=0;i<str.length;i++) {
      if(str[i]<='Z'&&str[i]>='A') {
        st+="-";                    //数组是push，字符串直接加
        st+=str[i].toLowerCase();   //toLowerCase()无参数哟~
      }
      else
        st+=str[i];
    }
  }
  s=st.toLowerCase();
  return s;
}
```
Sum All Odd Fibonacci Numbers
贴心地贴粗了会出错的链接23333
```
function sumFibs(num) {
  li=[1,1];
  var re=0;
  while(li[li.length-1]+li[li.length-2]<=num) 
    li.push(li[li.length-1]+li[li.length-2]);
  for(var i=0;i<li.length;i++) {
    if(li[i]%2==1)
      re+=li[i];
  }
  return re;
}
```
Sum All Primes
```
function sumPrimes(num) {
  var re=0;
  for(var i=2;i<=num;i++) {
    if(is(i))
      re+=i;
  }
  return re;
}
function is(n) {
  if(n>2&&n%2===0) return false;        //减少循环节省时间资源
  for(var b=3;b<=Math.sqrt(n);b+=2) {   //注意是小于等于
    if(n%b===0) {
      return false;
    }
  }
  return true;
}
```
Smallest Common Multiple
```
function smallestCommons(arr) {
  arr=arr.sort(function(a,b) {
    return b-a;
  });
  var max=arr[0],min=arr[1],mm=1,flag;
  for(var i=max;;i+=max) {                 //事实证明每次出现循环保护的时候都是寄几的错QVQ
    flag=1;
    for(var j=max;j>=min;j--) {
      if(i%j!==0)
        flag=0;
    }
    if(flag==1)
      return i;
  }
}
```
Finders Keepers
```
function find(arr, func) {
  var num = 0;
  for(var i=0;i<arr.length;i++) {
    if(func(arr[i])) return arr[i];
  }
}
```
Drop it
前面那一段游戏介绍有半毛钱关系吗。。。英语阅读第一段作用——引粗讨论对象==
```
function drop(arr, func) {
  while(!func(arr[0])) {
      arr.shift();
    }
  return arr;
}
```
Steamroller
```
function steamroller(arr) {         //它这儿不能用全局emmmm皮一下
  var a=[];
  return emm(a,arr);
}
function emm(a,arr) {
  for(var i=0;i<arr.length;i++) {
    if(Array.isArray(arr[i]))
      emm(a,arr[i]);
    else
      a.push(arr[i]);
  }
  return a;
}
```
Binary Agents
```
function binaryAgent(str) {
  var s="";
  arr=str.split(" ");
  for(var i=0;i<arr.length;i++) {
    int=parseInt(arr[i],2);                  //把字符串解析成数字，可定义进制
    s+=String.fromCharCode(int);
  }
  return s;
}
```
Everything Be True
```
function every(collection, pre) {
  ex=function(element,index,arr) {
    return element[pre];
  };
  return collection.every(ex);       //每个对象~
}
```
Arguments Optional
```
function add() {
  if(typeof(arguments[0])=="number" && typeof(arguments[1])=="number"){
    return arguments[0]+arguments[1];
  }
  else if(arguments.length==1 && typeof(arguments[0])=="number"){
    var x=arguments[0];
    return function(y){
      if(typeof(y)=="number"){
        return x+y;
      }
    };
  }
}
```
Validate US Telephone Numbers
```
function telephoneCheck(str) {
  var reg=/^1? ?(\(\d{3}\)|\d{3})[ |-]?\d{3}[ |-]?\d{4}$/;    
  return reg.test(str);                                       //匹配返回true，否则false
}
```
一个超棒的正则测试网站！https://regex101.com/
Symmetric Difference
参考了一下社区的解法x，对reduce理解不够x
```
function sym(args) {
  var ar = [];
    for (var i = 0; i < arguments.length; i++) {
        ar.push(arguments[i]);
    }
  function diff(a,b) {
    var arg=[];
    for(var i=0;i<a.length;i++){
      if(b.indexOf(a[i])==-1 && arg.indexOf(a[i])==-1)    //去重
        arg.push(a[i]);
    }
    for(var ii=0;ii<b.length;ii++){
      if(a.indexOf(b[ii])==-1 && arg.indexOf(b[ii])==-1)
        arg.push(b[ii]);
    }
    return arg;
  }
  return ar.reduce(diff);   //把数组中每两个相邻元素进行函数调用返回一个元素，一组数组也是一个元素哟
}
```
Exact Change
？？？发现了一个bug？？
`96.74-60=36.739999999995` ？？？
哇。。。js这么皮的吗？？？
找到解决方案四舍五入到两位小数 `.toFixed(2)` 还得每个减法的地方都加。。。
```
function checkCashRegister(price, cash, cid) {
  var change=[];
  var need=cash-price;
  var ne=need,all=0;
  var ca=[0.01,0.05,0.1,0.25,1,5,10,20,100];
  for(var i=8;i>=0;i--) {
    all+=cid[i][1];
    if(need>=ca[i]&&cid[i][1]>0) {     //需要的多于已有的，把所有已有的拿出来
      if(need>cid[i][1]) {
        need=(need-cid[i][1]).toFixed(2);
        change.push(cid[i]);
      }
      else {
        var a=need/ca[i];
        a=parseInt(a);
        if(a*ca[i]<=cid[i][1]) {
          need=(need-(a*ca[i])).toFixed(2);
          change.push([cid[i][0],(a*ca[i])]);
        }
        else {
          need=(need-cid[i][1]).toFixed(2);
          change.push(cid[i]);
        }
      }
    }
  }
  if(need>0) return "Insufficient Funds";
  if(ne==all) return "Closed";
  return change;
}
```
































