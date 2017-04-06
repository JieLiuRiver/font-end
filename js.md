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

## 关闭本页会弹出窗口
    <body onunload=leaveWindow()>

    <script>
        function leaveWindow(){
            window.open('http://www.263.net.cn','','toolbar=no, menubar=yes, location=no, width=260, height=240');
        }
    </script>
    </body>


## 显示时间
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

## 全部选取
    <form name="text">
        <input type=button value="全部选取" onclick="SelectAll('text.select')"><br>
        <textarea name="select" rows=10 cols=20>请在此输入您的建议：</textarea>
    </form>
    function SelectAll(FieldArea) {
        var tempval=eval("document."+FieldArea)
        tempval.focus()
        tempval.select()
    }


## 文本框中控制输入字数
    <textarea name=message wrap=physical rows=5 cols=30  onKeyDown="MaxInput(this.form)" onKeyUp="MaxInput(this.form)"></textarea>
    <input readonly type=text name=TLength size=3  value="100">个字符</font>
    maxLength = 99;
    function MaxInput(form) {
        if (form.message.value.length > maxLength)
        form.message.value = form.message.value.substring(0, maxLength);
        else form.TLength.value = maxLength - form.message.value.length;
    }

## 替换空格
    function replaceSpace(str)
    {
        return str.replace(/\s/g,'%20');
    }

## 斐波那契数列
    输入整数n，输出斐波那契数列第n项
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


## SQL
    SQL是Struc-tured Query Language（结构化查询语言）的缩写。SQL是一种专门用来与数据库沟通的语言
### 主键
    唯一标识表中每行的这个列（或这几列）称为主键。
    主键用来表示一个特定的行。没有主键，更新或删除表中特定行就极为困难，
    因为你不能保证操作只涉及相关的行。

### 检索列
    SELECT prod_name FROM Products;
    SELECT prod_id, prod_name, prod_price FROM Products;


### 只返回不同（具有唯一性）的行
    SELECT DISTINCT
    loadstationname
    FROM
    consignnote

### 返回不超过5行数据
    SELECT
    loadstationname
    FROM
    consignnote
    LIMIT 5

### 返回从第5行开始的8行数据
    SELECT
    loadstationname
    FROM
    consignnote
    LIMIT 8 OFFSET 5

### 注释
    SELECT prod_name    -- 这是一条注释
    FROM Products;

    # 这是一条注释
    SELECT
    prod_name
    FROM
    Products;

### 排序查询
    SELECT prod_name
    FROMO Products
    ORDER BY prod_name

    SELECT prod_id, prod_price, prod_name
    FROM Products
    ORDER BY prod_price, prod_name


### 价格降序来排序产品（最贵的排在最前面）
    SELECT prod_id, prod_price, prod_name
    FROM Products
    ORDER BY prod_price DESC;

    （ASC代表升序，默认升序）

### 过滤查询
    SELECT prod_name, prod_price FROM Products WHERE prod_price = 3.49;

    SELECT prod_id, prod_price, prod_name
    FROM Products
    WHERE vend_id = 'DLL01' AND prod_price <= 4;

    SELECT prod_name, prod_price
    FROM Products
    WHERE vend_id = 'DLL01' OR vend_id = ‘BRS01’;

    SELECT prod_name, prod_price FROM Products
    WHERE (vend_id = 'DLL01' OR vend_id = 'BRS01') AND prod_price >= 10;

    SELECT prod_name, prod_price FROM Products
    WHERE vend_id IN ( 'DLL01', 'BRS01' ) ORDER BY prod_name;
    相当于=>
    SELECT prod_name, prod_price FROM Products
    WHERE vend_id = 'DLL01' OR vend_id = 'BRS01' ORDER BY prod_name;

    # 列出除DLL01之外的所有供应商制造的产品
    SELECT prod_name FROM Products
    WHERE NOT vend_id = 'DLL01' ORDER BY prod_name;


### 使用通配符过滤
    为在搜索子句中使用通配符，必须使用LIKE操作符。
    LIKE指示DBMS，后跟的搜索模式利用通配符匹配而不是简单的相等匹配进行比较。
    通配符搜索只能用于文本字段（串），非文本数据类型字段不能使用通配符搜索。

    # 检索任意以Fish起头的词。%告诉DBMS接受Fish之后的任意字符，不管它有多少字符。
    SELECT prod_id, prod_name
    FROM Products WHERE prod_name LIKE 'Fish%';

    # 找出所有名字以J或M起头的联系人
    SELECT cust_contact
    FROM Customers WHERE cust_contact
    LIKE '[JM]%' ORDER BY cust_contact;、


### 字段组合
    # 返回是这样的： '何柳杰/17017271200'
    SELECT Concat(enlinkername, ' /', enlinkerphone)
    FROM consignnote

### 算术计算
     #汇总（单价乘数量）
     SELECT
     	totalqty,
     	totalfare,
     	totalqty * totalfare AS expanded_fare
     FROM consignnote

### 函数处理数据
     # 转换大写
     SELECT
        vend_name,
        UPPER(vend_name) AS vend_name_upcase
     FROM Vendors ORDER BY vend_name;

### 求平均值
     SELECT
     	AVG(totalfare) AS avg_totalfare
     FROM
     	consignnote

### 总数
     SELECT
        COUNT(*) AS num_cust
     FROM
        Customers;

### 最大值
     SELECT
        MAX(prod_price) AS max_price
     FROM
        Products;

     # MIN()最小值

### 返回购物品总数
     # OrderItems包含订单中实际的物品，每个物品有相应的数量，
     SELECT
        SUM(quantity) AS items_ordered
     FROM OrderItems
     WHERE order_num = 20005;

### 子查询
    # 获取产品名为'苹果'的订单号
    SELECT ordernum
    FROM orderitem
    WHERE productname = '苹果'

    #返回 1023,1024

    #根据订单号，获取对应的客户名
    SELECT customername
    FROM order
    WHERE ordernum IN (1023, 1024)

    =======》 等同于 子查询
    SELECT customername
    FROM order
    WHERE ordernum IN (
            SELECT ordernum
            FROM orderitem
            WHERE productname = '苹果'
        );
