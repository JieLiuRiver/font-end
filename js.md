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


