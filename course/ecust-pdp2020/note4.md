# 程序设计实践 4：AJAX

> 课程：[程序设计实践 2020 春](./index)

## Hello AJAX

<img src=".\img\image-20200427145128467.png" alt="Google 搜索候选" style="zoom: 33%;" />

AJAX 就是异步 JavaScript 和 XML 技术，在 2005 年用在了 Google 的搜索候选上从而流行起来。当你在搜索框输入到一半，还没有点击按钮或者敲击回车的时候，下方的列表里就会给出候选词。

首先我们知道，JavaScript 是可以操纵 HTML 标签的

```html
<p id="text"></p>
<script>
    document.getElementById("text").innerHTML = "hello"
</script>
```

我们可以用这种方法修改页面。

## XMLHttpRequest

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

## 例子

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
...

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