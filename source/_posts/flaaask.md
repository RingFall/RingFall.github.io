---
title: flaaask
date: 2019-11-28 09:32:29
tags:
thumbnail: "https://s2.ax1x.com/2020/02/16/3pvPc4.png"
---

每天菜菜循环～

还是好好学习叭orz

首先是一直想入坑的flask记录～看了文档觉得好简单？然后看了几个实例发现完全不。。。qaq

于是看了传说中的狗书，的确可以，感觉是文档加强版，变得更通俗并且加了必要的对与flask特性的解释，和插件！

（只是记录，没有逻辑x

---

生成requirements：`pip install pipreqs` ，在项目根目录 `pipreqs ./ --encoding=utf8`

freeze会生成所有滴

---

路由：url - endpoint - view function

使用 app.route 修饰器或者非修饰器形式的 app.add_url_rule() 生成映射。

---

`@property` 能把某个方法转换成属性，每次访问属性的时候，它都会执行底层的方法作为结果返回。
`@cached_property` 也一样，区别是只有第一次访问的时候才会调用底层的方法，后续的方法会直接使用之前返回的值。

---

Falsk 使用上下文让特定的变量在一个线程中全局可访问，与此同时却不会干扰其他线程。（current_app/g//request/session）

但是要app.app_context()调用push之后才能获取～

---

想必大家都发现了第一下栗子里的一个视图函数都贼鸡儿简单，所以当逻辑变得复杂时，此时需要在请求前后有一些固定的代码执行，这就系——**钩子**！

- before_first_request：注册一个函数，在处理第一个请求之前运行。
- before_request：注册一个函数，在每次请求之前运行。
- after_request：注册一个函数，如果没有未处理的异常抛出，在每次请求之后运行。
- teardown_request：注册一个函数，即使有未处理的异常抛出，也在每次请求之后运行。

---

Jinja2 支持宏和模板继承。宏类似于 Python 代码中的函数，导入宏：`&#123;% import 'macros.html' as macros %\&#125;`

需要在多处重复使用的模板代码片段可以写入单独的文件，再包含在所有模板中，以避免 重复： `&#123;% include 'common.html' %\&#125;` 

继承就不用嗦啦，改块的时候记得加super

变量可以使用过滤器～比如safe和capitalize之类哒。

用flask-bootstrap之后居然可以直接导入qvq神奇鸭

动态路由跳转用url_for()，视图函数名+动态部分或额外参数作为关键字参数传入。

---

Moment处理时间～还有自动fresh获取相对时间～～～

---

wtf库。。真的怎么看怎么是那个意思orz

---

发现了为啥有些登陆要用重定向回同一个view函数而不是直接接收post：

> 用户输入名字后提交表单，然后点击浏览器的刷新按钮，会看到一个莫名其妙的警告，要求在再次提交表单之前进行确认。之所以出现这种情况，是因为刷新页面时浏览器会重新发送之前已经发送过的最后一个请求。如果这个请求是一个包含表单数据的 POST 请求，刷新页面后会再次提交表单。
>
> 这种需求的实现方式是，使用重定向作为 POST 请求的响应，而不是使用常规响应。重定向是一种特殊的响应，响应内容是 URL，而不是包含 HTML 代码的字符串。浏览器收到这种响应时，会向重定向的 URL 发起 GET 请求，显示页面的内容。这个页面的加载可能要多花几微秒，因为要先把第二个请求发给服务器。除此之外，用户不会察觉到有什么不 同。现在，最后一个请求是 GET 请求，所以刷新命令能像预期的那样正常使用了。这个技 巧称为 Post/ 重定向 /Get 模式。

---

好的前半部分就是文档的解释版，后面从工厂函数开始要向大型项目进发辣！

导入扩展后，create_app() 函数就是程序的工厂函数，接受一个参数，是程序使用的配置名。程序创建并配置好后，就能初始化扩展了。在之前创建的扩展对象上调用 init_app() 可以完成初始化过程。

然后就是blueprint。程序包中创建了一个子包，用于保存蓝本。通过实例化一个 Blueprint 类对象可以创建蓝本。这个构造函数有两个必须指定的参数： 蓝本的名字和蓝本所在的包或模块。和程序一样，大多数情况下第二个参数使用 Python 的 \__name__ 变量即可。蓝本在工厂函数 create_app() 中注册到程序上。

---

不知不觉看完了？？后面讲的都是啥鸭orz

好的现在开始！journal项目～

---

导入的时候flask.ext.xxx根本是不存在的，神他喵已经被弃用了，直接from flask_xxx就行。记得要在对应虚拟环境中sudo pip install～

在app/init中初始化创建工厂函数create_app，把扩展都实例化且init一下～

在app/main/init中创建蓝本，末尾导入当前目录下模块（避免循环导入依赖）

然后肥到app/init中导入并注册蓝本就好啦

---

注册程序全局的错误处理程序，必须使用 @app_errorhandler~

---

天哪噜！窝之前安装的包居然都是全局的？？？枯了呜呜呜。都是zsh的错？进虚拟环境也没个提示orz说好的提示呢qaq

---

TBC。。。