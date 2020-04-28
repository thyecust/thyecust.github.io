# 程序设计实践 1：ASP 和 VBScript 基础

> 课程：[程序设计实践 2020 春](./index)

## Hello World

VBScript 可以用 `<% ... %>` 写在 `.asp` 文件里，也可以用 `<script language=vbscript runat=server>` 来写

```html
<script language=vbscript runat=server>
    response.write("hello")
</script>
```

下面用 `<%%>` 写。

## 变量

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
...
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

## 过程

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

## 条件

我们有三种条件

```asp
if ... then ... end if
if ... then ... (elif ... then...) end if
select case ... (case ... ...) end select
```

## 循环

### for ... to ... next

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

### for each ... in ... next

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

### do ... loop

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

## #include

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