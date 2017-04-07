## 原型prototype

### javascript的方法可以分为三类：
          1. 类方法
          2. 对象方法
          3. 原型方法

        例子:
        function People(name)
        {
          this.name=name;
          //对象方法
          this.Introduce=function(){
            alert("My name is "+this.name);
          }
        }
        //类方法
        People.Run=function(){
          alert("I can run");
        }
        //原型方法
        People.prototype.IntroduceChinese=function(){
          alert("我的名字是"+this.name);
        }

        //测试

        var p1=new People("Windking");

        p1.Introduce();

        People.Run();

        p1.IntroduceChinese();

### 关闭本页会弹出窗口
    <body onunload=leaveWindow()>

    <script>
        function leaveWindow(){
            window.open('http://www.263.net.cn','','toolbar=no, menubar=yes, location=no, width=260, height=240');
        }
    </script>
    </body>


### 显示时间
    function ButtonClock() {
    day = new Date();
    HourNow = day.getHours();
    MinuteNow = day.getMinutes();
    SecondNow = day.getSeconds();
    TimeNow = day.getTime();
    if (HourNow == 0) {hour = 12;ap = " am";}
    else if(HourNow <= 11) {ap = " am";hour = HourNow;}
         else if(HourNow == 12) {ap = " pm";hour = 12;}
              else if (HourNow >= 13) {hour = (HourNow - 12);ap = " pm";}
    if (HourNow >= 13) {hour = HourNow - 12;}
    if (MinuteNow <= 9) {minute = "0" + MinuteNow;}
    else (minute = MinuteNow)
    if (SecondNow <= 9) {second = "0" + SecondNow;}
    else {second = SecondNow;}
    time = hour + ":" + minute + ":" + second + ap;
    document.form.button.value = time;
    self.status = time;
    setTimeout('ButtonClock()', 1000);
    }

### 全部选取
    <form name="text">
        <input type=button value="全部选取" onclick="SelectAll('text.select')"><br>
        <textarea name="select" rows=10 cols=20>请在此输入您的建议：</textarea>
    </form>
    function SelectAll(FieldArea) {
        var tempval=eval("document."+FieldArea)
        tempval.focus()
        tempval.select()
    }


### 文本框中控制输入字数
    <textarea name=message wrap=physical rows=5 cols=30  onKeyDown="MaxInput(this.form)" onKeyUp="MaxInput(this.form)"></textarea>
    <input readonly type=text name=TLength size=3  value="100">个字符</font>
    maxLength = 99;
    function MaxInput(form) {
        if (form.message.value.length > maxLength)
        form.message.value = form.message.value.substring(0, maxLength);
        else form.TLength.value = maxLength - form.message.value.length;
    }

### 替换空格
    function replaceSpace(str)
    {
        return str.replace(/\s/g,'%20');
    }


### 斐波那契数列
    需求： 输入整数n，输出斐波那契数列第n项
    function Fibonacci(n){
        var arr = [];
        arr[0] = 0;
        arr[1] = 1;
        for(var i = 2; i <= n; i++) {
            arr[i] = arr[i - 1] + arr[i - 2];
        }
        return arr[n];
    }

### 台阶
    一只青蛙一次可以跳上1级，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法。
    得出的是一个斐波那契数列
    n=1, f(n)=1
    n=2, f(n)=2
    n>2,且为整数, f(n)=f(n-1)+f(n-2)

    function jumpFloor(number)
    {
        if (number<0){
            return -1;
        }else if(number <=2){
            return number
        }
        var arr = [];
        arr[0] = 1;
        arr[1] = 2;
        for(var i = 2; i < number; i++) {
            arr[i] = arr[i - 1] + arr[i - 2];
        }
        return arr[number-1];
    }


###  作用域
    作用域是一套规则，用于确定在何处以及如何查找变量（标识符）。如果查找的目的是对
    变量进行赋值，那么就会使用 LHS 查询；如果目的是获取变量的值，就会使用 RHS 查询。
    赋值操作符会导致 LHS 查询。 ＝ 操作符或调用函数时传入参数的操作都会导致关联作用域
    的赋值操作。
    JavaScript 引擎首先会在代码执行前对其进行编译，在这个过程中，像 var a = 2 这样的声
    明会被分解成两个独立的步骤：
    1. 首先， var a 在其作用域中声明新变量。这会在最开始的阶段，也就是代码执行前进行。
    2. 接下来， a = 2 会查询（LHS 查询）变量 a 并对其进行赋值。
    LHS 和 RHS 查询都会在当前执行作用域中开始，如果有需要（也就是说它们没有找到所
    需的标识符），就会向上级作用域继续查找目标标识符，这样每次上升一级作用域（一层
    楼），最后抵达全局作用域（顶层），无论找到或没找到都将停止。
    不成功的 RHS 引用会导致抛出 ReferenceError 异常。不成功的 LHS 引用会导致自动隐式
    地创建一个全局变量（非严格模式下），该变量使用 LHS 引用的目标作为标识符，或者抛
    出 ReferenceError 异常（严格模式下）。

### 词法作用域
    JavaScript 中有两个机制可以“欺骗”词法作用域： eval(..) 和 with 。前者可以对一段包
    含一个或多个声明的“代码”字符串进行演算，并借此来修改已经存在的词法作用域（在
    运行时）。后者本质上是通过将一个对象的引用当作作用域来处理，将对象的属性当作作
    用域中的标识符来处理，从而创建了一个新的词法作用域（同样是在运行时）。
    这两个机制的副作用是引擎无法在编译时对作用域查找进行优化，因为引擎只能谨慎地认
    为这样的优化是无效的。使用这其中任何一个机制都将导致代码运行变慢。不要使用它们。


### 函数作用域、块作用域
    函数是 JavaScript 中最常见的作用域单元。本质上，声明在一个函数内部的变量或函数会
    在所处的作用域中“隐藏”起来，这是有意为之的良好软件的设计原则。
    但函数不是唯一的作用域单元。块作用域指的是变量和函数不仅可以属于所处的作用域，
    也可以属于某个代码块（通常指 { .. } 内部）。
    从 ES3 开始， try/catch 结构在 catch 分句中具有块作用域。
    在 ES6 中引入了 let 关键字（ var 关键字的表亲），用来在任意代码块中声明变量。 if
    (..) { let a = 2; } 会声明一个劫持了 if 的 { .. } 块的变量，并且将变量添加到这个块
    中。
    有些人认为块作用域不应该完全作为函数作用域的替代方案。两种功能应该同时存在，开
    发者可以并且也应该根据需要选择使用何种作用域，创造可读、可维护的优良代码


### 提升
    我们习惯将 var a = 2; 看作一个声明，而实际上 JavaScript 引擎并不这么认为。它将 var a
    和 a = 2 当作两个单独的声明，第一个是编译阶段的任务，而第二个则是执行阶段的任务。
    这意味着无论作用域中的声明出现在什么地方，都将在代码本身被执行前首先进行处理。
    可以将这个过程形象地想象成所有的声明（变量和函数）都会被“移动”到各自作用域的
    最顶端，这个过程被称为提升。
    声明本身会被提升，而包括函数表达式的赋值在内的赋值操作并不会提升。
    要注意避免重复声明，特别是当普通的 var 声明和函数声明混合在一起的时候，否则会引
    起很多危险的问题！


## 闭包
    当函数可以记住并访问所在的词法作用域，即使函数是在当前词法作用域之外执行，这时
    就产生了闭包。
    如果没能认出闭包，也不了解它的工作原理，在使用它的过程中就很容易犯错，比如在循
    环中。但同时闭包也是一个非常强大的工具，可以用多种形式来实现模块等模式。
    模块有两个主要特征：（1）为创建内部作用域而调用了一个包装函数；（2）包装函数的返回
    值必须至少包括一个对内部函数的引用，这样就会创建涵盖整个包装函数内部作用域的闭
    包。

### this
    如果不使用 this ，那就需要给函数显式传入一个上下文对象
    This 提供了一种更优雅的方式来隐式“传递”一个对象引用，因此可以将 API 设计
    得更加简洁并且易于复用。
    随着你的使用模式越来越复杂，显式传递上下文对象会让代码变得越来越混乱，使用 this
    则不会这样。当我们介绍对象和原型时，你就会明白函数可以自动引用合适的上下文对象
    有多重要。

    当一个函数被调用时，会创建一个活动记录（有时候也称为执行上下文）。这个记录会包
    含函数在哪里被调用（调用栈）、函数的调用方法、传入的参数等信息。 this 就是记录的
    其中一个属性，会在函数执行的过程中用到

    如果要判断一个运行中函数的 this 绑定，就需要找到这个函数的直接调用位置。找到之后
    就可以顺序应用下面这四条规则来判断 this 的绑定对象。
    1. 由 new 调用？绑定到新创建的对象。
    2. 由 call 或者 apply （或者 bind ）调用？绑定到指定的对象。
    3. 由上下文对象调用？绑定到那个上下文对象。
    4. 默认：在严格模式下绑定到 undefined ，否则绑定到全局对象

### 对象
    JavaScript 中的对象有字面形式（比如 var a = { .. } ）和构造形式（比如 var a = new
    Array(..) ）。字面形式更常用，不过有时候构造形式可以提供更多选项。
    对象就是键 / 值对的集合。可以通过 .propName 或者 ["propName"] 语法来获取属性值。访
    问属性时，引擎实际上会调用内部的默认 [[Get]] 操作（在设置属性值时是 [[Put]] ），
    [[Get]] 操作会检查对象本身是否包含这个属性，如果没找到的话还会查找 [[Prototype]]

### 类
    类的另一个核心概念是多态，这个概念是说父类的通用行为可以被子类用更特殊的行为重
    写。实际上，相对多态性允许我们从重写行为中引用基础行为。“类”和“实例”的概念来源于房屋建造

    类是一种设计模式。许多语言提供了对于面向类软件设计的原生语法。JavaScript 也有类
    似的语法，但是和其他语言中的类完全不同。
    类意味着复制。
    传统的类被实例化时，它的行为会被复制到实例中。类被继承时，行为也会被复制到子类
    中。
    多态（在继承链的不同层次名称相同但是功能不同的函数）看起来似乎是从子类引用父
    类，但是本质上引用的其实是复制的结果。
    JavaScript 并不会（像类那样）自动创建对象的副本。

### 构造函数
    类实例是由一个特殊的类方法构造的，这个方法名通常和类名相同，被称为构造函数。这
    个方法的任务就是初始化实例需要的所有信息（状态）
    类构造函数属于类，而且通常和类同名。此外，构造函数大多需要用 new 来调，这样语言
    引擎才知道你想要构造一个新的类实例。

### 继承
    定义好一个子类之后，相对于父类来说它就是一个独立并且完全不同的类。子类会
    包含父类行为的原始副本，但是也可以重写所有继承的行为甚至定义新行为。

### 多态
    class Vehicle {
    engines = 1
    ignition() {
    output( "Turning on my engine." );
    }
    drive() {
    ignition();
    output( "Steering and moving forward!" )
    }
    }
    class Car inherits Vehicle {
    wheels = 4
    drive() {
    inherited:drive()
    output( "Rolling on all ", wheels, " wheels!" )
    }
    }
    class SpeedBoat inherits Vehicle {
    engines = 2
    ignition() {
    output( "Turning on my ", engines, " engines." )
    }
    pilot() {
    inherited:drive()
    output( "Speeding through the water with ease!" )
    }
    }
    Car 重写了继承自父类的 drive() 方法，但是之后 Car 调用了 inherited:drive() 方法，
    这表明 Car 可以引用继承来的原始 drive() 方法。快艇的 pilot() 方法同样引用了原始
    drive() 方法。


### 从输入网址到显示网页的过程分析
    1、浏览器中输入网址。
    2、发送至DNS服务器并获得域名对应的WEB服务器的ip地址。
    3、与WEB服务器建立TCP连接。
    4、浏览器向WEB服务器的ip地址发送相应的http请求。
    5、WEB服务器响应请求并返回指定URL的数据，或错误信息，如果设定重定向，则重定向到新的URL地址。
    6、浏览器下载数据后解析HTML源文件，解析的过程中实现对页面的排版，解析完成后在浏览器中显示基础页面。
    7、分析页面中的超链接并显示在当前页面，重复以上过程直至无超链接需要发送，完成全部显示。

    连接3次握手简述：
        客户端需要确认服务端有没有空为我服务？
        我需要问小明有没有空一起玩lol？
            我: 小明，玩游戏？
            小明： 好，来来来！
            我： ok，我建房间。


    关闭连接四次挥手：
        客户端要断开连接
        我要下班回家
            我： 到点了，一起下班走吧
            小伙子： 好，我们的工作做完了，等一下我。
            ...1h后
            小伙子： 好了，我们走吧
            我： 走走走...

### Doctype作用
    其实就是告诉浏览器用什么用模式去解析文档， 使用doctype可以避免浏览器到怪异模式， 如果说页面没有DOCTYPE声明,浏览器会使用怪异模式解析文档， 这意味着什么，意味着浏览器会按照自身浏览器的方式去解析渲染页面，在不同浏览器会有不同的样式，不同到表现，而这并不是我们希望看到的。

### 渐进增强跟优雅降级之间的区别
    其实渐进增强，比方说，先写一个简单功能的页面，能满足各版本浏览器，后面针对高级浏览器增加一些css3绚丽的功能，让整个的体验变得更加好， 因此这种方式更多的关注的是内容本身，这就是一个向上兼容到过程。
        而优雅降级呢，关注的就是高级的浏览器，以一种发展的眼光看待，例如，一开始，就实现出一个绚丽的功能，后面再针对低版本的浏览器进行向下兼容。这种方式，是更为常见到一种方式。

### 无样式内容闪烁
    其实指的是文档的样式闪烁。 造成闪烁的原因有2个：
        1.使用了@import方法导入css，  在IE下碰到这玩意，它会先去加载整个文档到DOM, 之后再去加载css，中间到这个过程，文档样式是从无到有的一个过程。
        2.样式表放在文档页面到不同位置，IE5/6会造成页面闪烁，应该把样式表放在head中。

### href传递中文，get 方式请求中文乱码问题
    href传递中文可以这样用： escape(field)方法处理中文
    使用unescape()方法还原

    对于get方式请求，js可以对整个url进行一次： encodeURI(url)处理, 把字符串作为 URI 进行编码,例如：
        document.write(encodeURI("http://www.w3school.com.cn/My first/"))
        输出：http://www.w3school.com.cn/My%20first/
        如果 URI 组件中含有分隔符，比如 ? 和 #，　使用encodeURIComponent()

    还有一个方法： encodeURIComponent()， 作用是把字符串作为URI组件进行编码，例如：
    console.log( encodeURIComponent("http://www.helijie.com/blog") )
        输出：
            http%3A%2F%2Fwww.heliujie.com%2Fblog

    获取到url上经过encodeURIComponent()处理的参数后，需要转换， 使用方法：
        decodeURIComponent( param )

### css动画与js动画之间的区别
    总体而言，对于简单的动画，不需要中间过程控制的动画，不需要太多条件控制的动画，使用css动画。 相反，对于复杂的动画，需要控制中间流程的动画，应该使用js动画这样可以控制工作流。
        其实如果我们使用js写动画，它的控制能力很强，不会有什么兼容性，而css则有兼容问题

### 写一个匹配特殊字符的正则
    /((?=[\x21-\x7e]+)[^A-Za-z0-9])/.test('#%43#*#&*#^&*#')
        1.小括号()代表一个子表达式的开始和结束的位置
        2.问好?意味着会匹配前面的子表达式零次或者一次
        3.中括号[],  意思是一个中括号表达式的开始
        4.(?=pattern), 意思是匹配到pattern的字符串，它的开始处进行匹配查找字符串
        5. \xn匹配n， n是十六进制转义值，必须是2个数字长
        6.+号匹配前面的子表达式一次或者多次
        7.[^A-Z]匹配任何不在A-Z范围内的任意字符


### 计算字符串的字节长度
    function getLenByReg(str){
        var result = 0;
        for (var i = 0; i < str.length; i++) {
            var reg = (/[^\x00-\xff]/ig);
            if (reg.test(str[i])) {
                result += 2;
            } else {
                result += 1;
            }
        }
        return result;
    }


### iframe跨域访问
    由于浏览器同源策略，凡是发送请求url的协议、域名、端口三者之间任意一与当前页面地址不同即为跨域。
    document.getElementById("myIFrame").contentWindow.document
    只有在同源的情况下，父窗口和子窗口才能通信；如果跨域，就无法拿到对方的DOM
    window.parent.document.body
    对于完全不同源的网站，目前有4种方法，可以解决跨域窗口的通信问题
        1. 片段识别符
            指的是，URL的#号后面的部分，
            比如http://example.com/x.html#fragment的#fragment,
            如果只是改变片段标识符，页面不会重新刷新,
            父窗口可以把信息，写入子窗口的片段标识符
            var src = originURL + '#' + data; document.getElementById('myIFrame').src = src;
            子窗口通过监听hashchange事件得到通知
            window.onhashchange = checkMessage;
            function checkMessage() {
              var message = window.location.hash;
              // ...
            }
            子窗口也可以改变父窗口的片段标识符
            parent.location.href= target + “#” + hash;

        2. 跨文档通信API
           HTML5为了解决这个问题，引入了一个全新的API
           window对象新增了一个window.postMessage方法，允许跨窗口通信，不论这两个窗口是否同源
           父窗口aaa.com向子窗口bbb.com发消息，调用postMessage方法就可以了
           var popup = window.open('http://bbb.com', 'title');
           popup.postMessage('Hello World!', 'http://bbb.com');
           postMessage方法的第一个参数是具体的信息内容，第二个参数是接收消息的窗口的源（origin），
           即“协议 + 域名 + 端口”。也可以设为*，表示不限制域名，向所有窗口发送
           子窗口向父窗口发送消息的写法类似
           window.opener.postMessage('Nice to see you', 'http://aaa.com');
           父窗口和子窗口都可以通过message事件，监听对方的消息
           window.addEventListener('message', function(e) {
              console.log(e.data);
           },false);

           message事件的事件对象event，提供以下三个属性
           1. event.source：发送消息的窗口
           2. event.origin: 消息发向的网址
           3. event.data: 消息内容

           子窗口通过event.source属性引用父窗口，然后发送消息
           window.addEventListener('message', receiveMessage);
           function receiveMessage(event) {
              event.source.postMessage('Nice to see you!', '*');
           }

           window.addEventListener('message', receiveMessage);
            function receiveMessage(event) {
              if (event.origin !== 'http://aaa.com') return;
              if (event.data === 'Hello World') {
                  event.source.postMessage('Hello', event.origin);
              } else {
                console.log(event.data);
              }
            }

        3. JSONP
            这种方式主要是通过动态插入一个script标签。浏览器对script的资源引用没有同源限制，同时资源加载到页面后会立即执行（没有阻塞的情况下）。

            var _script = document.createElement('script');
            _script.type = 'text/javascript';
            _script.src = "http://localhost8888/jsonp?callback=f";
            var head = document.getElemenetByTagName('head')[0];
            head.appendChild(_script);

         4. 通过修改document.domain来跨子域
            跨域限制
                限制之一： 不能通过ajax的方法去请求不同源中的文档
                限制之二： 浏览器中不同域的框架之间是不能进行js的交互操作的
            不同的框架 之间（父子或同辈），是能够获取到彼此的window对象
            不能使用获取到的window对象的属性和方法（html5中的 postMessage方法是一个例外）

            父页面：(设置document.domain)
                <iframe src="http://abc.com/a.html" if="iframe" onload="test()"></iframe>
                <script>
                    document.domain = 'abc.com';
                    function test() {
                        console.log('子域window', document.getElementById('iframe').contentWindow);
                    }
                </script>

            子页面：（也要设置）
                document.domain = 'abc.com';

            这样我们就可以通过js访问到iframe中的各种属性和对象了

### Cookie, LocalStorage, SessionStorage 之间的区别
    Web storage 有2种形式
        1. LocalStorage
        2. SessionStorage
        通过js设置值， 当页面重新刷新后，依然能获取到。跟cookie比较起来，localstorage安装在客户端，不需要请求服务请数据。
        sessionstorage保存在window对象中，关闭窗口，数据销毁。
        1. localStorage.length
        2. localStorage.setItem(key, value)
        3. localStorage.getItem(key)
        4. localStorage.key(n)
        5. localStorage.removeItem()
        6. localStorage.clear()


### 关于 script defer script async
    <script src="script.js"></script>
    没有 defer 或 async，浏览器会立即加载并执行指定的脚本，“立即”指的是在渲染该 script 标签之下的文档元素之前，也就是说不等待后续载入的文档元素，读到就加载并执行。
    <script async src="script.js"></script>
    有 async，加载和渲染后续文档元素的过程将和 script.js 的加载与执行并行进行（异步）。
    <script defer src="myscript.js"></script>
    有 defer，加载后续文档元素的过程将和 script.js 的加载并行进行（异步），但是 script.js 的执行要在所有元素解析完成之后，DOMContentLoaded 事件触发之前完成。

    把所有脚本都丢到 </body> 之前是最佳实践，因为对于旧浏览器来说这是唯一的优化选择，此法可保证非脚本的其他一切元素能够以最快的速度得到加载和解析


### 冒泡排序
    每一次对比相邻2个数据的大小，小的排在前面，如果前面数据大于后者，则交换位置。
     *    用2层for循环，外层第一个数到倒数第二个数，内层从外层的后一个数字到最后一个数字。
     *    1.简单实用易于理解
     *    2.比较次数多，效率较低
     function bubbleSort(arr){
         var len = arr.length;
         for (var i = 0; i < len - 1; i++) {
           for (var j = i + 1; j < len; j++) {
             if (arr[i] > arr[j]) {
               var temp = arr[i];
               arr[i] = arr[j];
               arr[j] = temp;
             }
           }
         }
         return arr;
       }


### 快速排序
    先找到一个基准点（一般指数组的中部），然后数组被该基准点分为两部分，依次与该基准点数据比较，如果比它小，放左边；反之，放右边,   左右分别用一个空数组去存储比较后的数据。最后递归执行上述操作，直到数组长度<=1
     *   1. 快速，常用
     *   2. 需要另外声明两个数组，浪费了内存空间资源
    function quickSort(arr){
          if(arr.length<=1){
              return arr;
          }
          var midIndex=Math.floor(arr.length/2);
          /* 取基准点的值,splice(index,1)函数可以返回数组中被删除的那个数arr[index+1] */
          var midIndexVal=arr.splice(midIndex,1);
          var left=[];
          var right=[];
          for(var i=0;i<arr.length;i++){
              if(arr[i]<midIndexVal){
                  left.push(arr[i]); // 比基准点小的放在左边数组
              }
              else{
                  right.push(arr[i]); // 比基准点大的放在右边数组
              }
          }
          /* 递归执行以上操作,对左右两个数组进行操作，直到数组长度为<=1；*/
          return quickSort(left).concat(midIndexVal,quickSort(right));
     };

### this指向问题
    var length = 10;
      function fn() {
        console.log(this.length);
      }
      var obj = {
        length: 5,
        method: function(fn) {
          fn();  // 10
          arguments[0]();  // 这里arguments[0],访问的是fn，对象访问可以用这种方式。 相当于arguments调用fn, 因此这里打印出2
        }
      };
      obj.method(fn, 1);


### 声明提前
    function fn(a) {
        console.log(a);
        var a = 2;
        function a() {}
        console.log(a);
      }
      fn(1);
      var 和 函数声明同时存在，函数声明优先级比较高，
      因此一进来，打印出的是 function a(){}; 接着往下执行，a被重新赋值，因此打印出2

### 局部变量和全局变量
      var f = true;
      if (f === true) {
        var a = 10;
      }
      function fn() {
        var b = 20;
        c = 30;
      }
      fn();
      console.log(a); // 10
      console.log(b); // 报错
      console.log(c); // 30

### 给字符串、数字上挂属性，并访问
      var a = 10;
      a.pro = 10;
      console.log(a.pro + a);
      a是一个数字，a下挂一个属性pro等于0， 不会报错，一旦访问，变成undefined, undefined + 10 => NaN

      var s = 'hello';
      s.pro = 'world';
      console.log(s.pro + s);
      undefined + 'hello' => "undefinedhello"

### 判断一个字符串中出现次数最多的字符，并统计次数
    function findStrMostTimes(str){
        var obj = {};
        var max = -1;
        var letter = '';
        for (var i = 0; i < str.length; i++) {
          if (typeof obj[str[i]] == 'undefined') {
            obj[str[i]] = 1;
          } else {
            obj[str[i]]++;
          }
          if (obj[str[i]] > max) {
            max = obj[str[i]];
            letter = str[i];
          }
        }
        console.log('letter', letter, 'times', max);
      }


### 去掉数组中重复的数字
     function uniqueArr(arr){
        for (var i = 0; i < arr.length; i++ ) {
            for (var j = i + 1; j < arr.length;) {
              if (arr[i] == arr[j]) {
                arr.splice(j, 1);
                j--;
              }
            }
        }
      }
      uniqueArr([1,2,4,2,1,5,6,3,3,2,3]);

### http://huaren-it.com/cat/%E5%88%B7%E9%A2%98/


### cookie读写删
    //JS操作cookies方法!

    //写cookies

    function setCookie(name,value)
    {
        var Days = 30;
        var exp = new Date();
        exp.setTime(exp.getTime() + Days*24*60*60*1000);
        document.cookie = name + "="+ escape (value) + ";expires=" + exp.toGMTString();
    }

    //读取cookies
    function getCookie(name)
    {
        var arr,reg=new RegExp("(^| )"+name+"=([^;]*)(;|$)");

        if(arr=document.cookie.match(reg))

            return unescape(arr[2]);
        else
            return null;
    }

    //删除cookies
    function delCookie(name)
    {
        var exp = new Date();
        exp.setTime(exp.getTime() - 1);
        var cval=getCookie(name);
        if(cval!=null)
            document.cookie= name + "="+cval+";expires="+exp.toGMTString();
    }
    //使用示例
    setCookie("name","hayden");
    alert(getCookie("name"));


### Flex布局是什么
    用来为盒状模型提供最大的灵活性。
    任何一个容器都可以指定为Flex布局。
    Webkit内核的浏览器，必须加上-webkit前缀。子元素的float、clear和vertical-align属性将失效。
    采用Flex布局的元素，称为Flex容器（flex container），简称"容器"。
    它的所有子元素自动成为容器成员，称为Flex项目（flex item），简称"项目"

### 柯里化
    function cury(fn){
        var args = Array.prototype.slice.call(arguments, 1);
        return function(){
            var innerArgus = Array.prototype.slice.call(arguments);
            var finArgus = args.concat(innerArgus);
            return fn.apply(null, finArgus);
        }
    }

### Bind函数
    function bind(fn, context){
        var args = Array.prototype.slice.call(arguments, 2);
        return function(){
            var innerArgus = Array.prototype.slice.call(arguments);
            var finArgus = args.concat(innerArgus);
            return fn.apply(context, finArgus);
        }
    }
