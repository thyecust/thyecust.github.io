---
typora-copy-images-to: img
---

# 程序设计实践 2020 春

> 这是华东理工大学计算机系（计算机科学与工程、软件工程专业）的第二门实践课，在大一下开展。第一门实践课讲 HTML、CSS、JavaScript，大作业是做静态网站。可以参考清华学堂在线公开课：前端攻城狮。

[toc]

## 课程介绍

![程序设计综合实践](C:\Users\tianh\Documents\GitHub\thyecust.github.io\course\ecust-pdp2020\img\image-20200427145815491.png)

内容

* HTML 表单和 ASP 编程
* 数据库设计
* 系统框架分析和实现
* 应用系统开发

参考资料

* w3schools
* 《网络程序设计——ASP》，尚俊杰
* 《数据库技术与应用基础——Access2010》，单颀 王芳

## ASP

ASP 是 Active Server Pages 的缩写，是一种 Web 编程的的开发框架，支持许多不同的开发模型

* 经典 ASP
* ASP.NET Web Forms
* ASP.NET MVC
* ASP.NET Web Pages
* ......

经典 ASP 是微软 1998 年推出的，是微软的第一个服务器端脚本语言，页面拓展名是 `.asp`，通常用 VBScript 写。

ASP.NET 是经典 ASP 的后继，在 2002 年推出，页面拓展名是 `.aspx`，通常用 C# 写。

这门课讲经典 ASP。

经典 ASP 可以用 JavaScript 写，例如

```asp
<%@ language="javascript"%>
<!DOCTYPE html>
<html>
    <body>
        <%
        Response.Write("Hello World!")
        %>
    </body>
</html>
```

这门课用 VBScript 写。

## VBScript

VBScript 可以用 `<% ... %>` 写在 `.asp` 文件里，也可以用 `<script language=vbscript runat=server>` 来写

```html
<script language=vbscript runat=server>
    response.write("hello")
</script>
```

下面用 `<%%>` 写。

### 变量

VBScript 是不区分大小写的，就算是变量名也不区分。

在 ASP 里，这样的代码

```asp
Dim val1
val2="Hello"
```

是不报错的，因为它自动定义了 `val2` 这个变量，我们可以用

```asp
<%@ language="vbscript"%>
<%Option Explicit '必须放在最前面 %> 
<!DOCTYPE html>
<html>
    <body>
        <%
        response.write("Hello World!")
        Dim val1
        val2="Hello"
        %>
    </body>
</html>
```

`Option Explicit` 就会禁止之前的自动定义，报错。

在 ASP 里可以定义一维和二维数组，索引从 `0` 开始

```asp
<%
Dim x(2,2)
x(0,0)="Volvo"
x(0,1)="BMW"
x(0,2)="Ford"
x(1,0)="Apple"
x(1,1)="Orange"
x(1,2)="Banana"
x(2,0)="Coke"
x(2,1)="Pepsi"
x(2,2)="Sprite"
for i=0 to 2
    response.write("<p>")
    for j=0 to 2
        response.write(x(i,j) & "<br />")
    next
    response.write("</p>")
next
%>
```

在一个 ASP 页面内，变量的声明周期还是很长的

```asp
<%
	if true then
        Dim val1
        val1="hello"
    end if
%>
<%
    response.write(val1)
%>
```

这样用没问题，但是如果要跨页面使用变量，就得定义成 Session 或者 Application 变量。

下面介绍了过程，你在一个过程内定义的变量，出了这个过程就没有了。Again，如果你没有使用 `Option Explicit`，虽然你引用了一个不存在的变量，也不会有任何的报错，程序会自动定义一个新的未经赋值的变量。

### 过程

可以用 `sub` 定义过程，用 `call` 调用

```asp
<%
	sub sum(val1,val2)
        response.write(val1+val2)
    end sub
%>
<%
    call sum(1,2)
%>
```

页面就会显示 `3`，也可以用 `sum 1,2` 调用。

也可以定义函数，如

```asp
<%
    function sum(val1,val2)
    sum=val1+val2
    end function
%>
<%
    =sum(1,2)
%>
```

效果和上一个例子一样。

如果用 JavaScript 写就是

```asp
<%
    function sum(val1,val2){
        Response.Write(val1+val2)
    }
%>
<%
    sum(1,2)
%>
```

这时查看页面的 HTML 是

```html
<!DOCTYPE html>
<html>
<body>
3
</body>
</html>
```

这说明这个过程是在服务器端执行的，在客户端我们只能得到结果，和直接在 HTML 里写 JavaScript 是不同的。

上面这个例子，你也可以写成

```html
<script  language="javascript" runat="server">
	function jsproc(num1,num2){
		Response.Write(num1+num2)
	}
</script>
```

`runat="server"` 这个属性也使得它在服务端执行，在客户端是看不见这段代码的。

### 条件

我们有三种条件

```asp
if ... then ... end if
if ... then ... (elif ... then...) end if
select case ... (case ... ...) end select
```

### 循环

#### for ... to ... next

```asp
for i=0 to 10 (step 2) ... next
```

`step` 可以是负数，例如

```asp
for i=10 to 0 step -2 ... next
```

在 for 循环内部可以写退出，如

```asp
for i=1 to 10
	response.write(i&"<br/>")
	exit for
next
```

在输出 `1` 之后就退出循环了，如果用 `if i=7 then exit if` 就可以在输出 `7` 之后退出循环。

#### for each ... in ... next

```
dim i(20),x
i(0)=0
i(1)=1
i(2)=2
for each x in i
	response.write(x&"<br/>")
next
```

因为 `i(3)` 和之后的元素都未赋值，所以输出是

```html
0<br/>1<br/>2<br/><br/><br/><br/><br/><br/><br/><br/><br/>
```

#### do ... loop

我们有好几种 do loop

```
do while i<10 ... loop
do ... loop while i<10
do until i=10 ... loop
do ... loop until i=10
```

do loop 也有退出，如

```
do until i=10
	i=i-1
	if i<10 then exit do
loop
```

### #include

最后，动态页面很重要的一个需求就是，把小的 ASP 页面插入到一个大页面里面去。例如第二周作业 2，在用户登录前后导航栏是不同的，可以这样实现

`index.asp`：

```asp
<% if logged=true then %>
    <!--#include file="logged.asp"-->
<% else %>
    <!--#include file="unlogged.asp"-->
<% end if %>
```

`logged.asp`：

```html
<p>Welcome</p>
```

``unlogged.asp`：

```html
<p>Log in please.</p>
```

在这个例子里，你可以把 `logged.asp` 改成 `logged.html` ，因为它是完全静态的。

这种 #include 方法也非常安全，因为你在客户端打开调试工具也只能看到 `index.asp` 这一个文件，内容是 `<p>Welcome</p>`，看不到它具体来源于哪一个文件。

## Session，Application

## AJAX

<img src="C:\Users\tianh\Documents\GitHub\thyecust.github.io\course\ecust-pdp2020\img\image-20200427145128467.png" alt="Google 搜索候选" style="zoom: 33%;" />

AJAX 就是异步 JavaScript 和 XML 技术，在 2005 年用在了 Google 的搜索候选上从而流行起来。当你在搜索框输入到一半，还没有点击按钮或者敲击回车的时候，下方的列表里就会给出候选词。

首先我们知道，JavaScript 是可以操纵 HTML 标签的

```html
<p id="text"></p>
<script>
    document.getElementById("text").innerHTML = "hello"
</script>
```

我们可以用这种方法修改页面。

### XMLHttpRequest

下一个问题就是，如何在不刷新页面的情况下和服务器通信呢？为了实现这个功能，发明了 `XMLHttpRequest` 这个对象，我们可以用它发送 HTTP 请求

```javascript
>> let xhttp = new XMLHttpRequest();
>> xhttp.open("GET","asp2020/hw/1");
>> xhttp.send();
>> xhttp.response;
<< "hello world"
```

查看这个请求的状态

```javascript
>> xhttp.status;
<< 200
```

`200` 意味着请求成功。

查看这个对象的状态

```javascript
>> xhttp.readyState;
<< 4
```

`4` 意味着请求已经发送，可以用 `response` 或者 `responseText` 属性查看回复信息了。

`XMLHttpRequest` 还有一个属性 `onreadystatechange`，是一个 Event Handler，当 `readyState` 发生变化的时候就会被调用。

### 例子

现在我们就可以写一个 AJAX 的页面了，例如

`index.asp`：

```asp
<html>
<head>
<script>
function showHint(str) {
    if (str.length == 0) {
        document.getElementById("txtHint").innerHTML = "";
        return;
    } else {
        var xmlhttp = new XMLHttpRequest();
        xmlhttp.onreadystatechange = function() {
            if (this.readyState == 4 && this.status == 200) {
                document.getElementById("txtHint").innerHTML = this.responseText;
            }
        };
        xmlhttp.open("GET", "gethint.asp?q=" + str);
        xmlhttp.send();
    }
}
</script>
</head>
<body>

<p><b>Start typing a name in the input field below:</b></p>
<form>
First name: <input type="text" onkeyup="showHint(this.value)">
</form>
<p>Suggestions: <span id="txtHint"></span></p>
</body>
</html>
```

`gethint.asp`：

```asp
<%
response.expires=-1
dim a(30)
a(1)="Anna"
a(2)="Brittany"
a(3)="Cinderella"
a(4)="Diana"
a(5)="Eva"
a(6)="Fiona"
a(7)="Gunda"
a(8)="Hege"
a(9)="Inga"
a(10)="Johanna"
a(11)="Kitty"
a(12)="Linda"
a(13)="Nina"
a(14)="Ophelia"
a(15)="Petunia"
a(16)="Amanda"
a(17)="Raquel"
a(18)="Cindy"
a(19)="Doris"
a(20)="Eve"
a(21)="Evita"
a(22)="Sunniva"
a(23)="Tove"
a(24)="Unni"
a(25)="Violet"
a(26)="Liza"
a(27)="Elizabeth"
a(28)="Ellen"
a(29)="Wenche"
a(30)="Vicky"

'ucase() 这个函数把所有字母都变成大写
q=ucase(request.querystring("q"))

if len(q)>0 then
  hint=""
  for i=1 to 30 
    '对所有候选词遍历
    if q=ucase(mid(a(i),1,len(q))) then
      '如果 q 和该候选词的前几位相同
      if hint="" then
        hint=a(i)
      else
        hint=hint & ", " & a(i)
      end if
    end if
  next
end if

if hint="" then
  response.write("no suggestion")
else
  response.write(hint)
end if
%>
```

## Web Pages

> 按照顺序下面应该是 ASP 连接数据库。在涉及到数据库的 Web 编程中，推荐 MVC 设计模式，但是经典 ASP 是比较陈旧的开发模型。所以下面介绍 Web Pages。