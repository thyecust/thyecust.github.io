---
typora-copy-images-to: img
---

# 程序设计实践 2020 春

> 这是华东理工大学计算机系（计算机科学与工程、软件工程专业）的第二门实践课，在大一下开展。第一门实践课讲 HTML、CSS、JavaScript，大作业是做静态网站。可以参考清华学堂在线公开课：前端攻城狮。

## 课程介绍

![程序设计综合实践](.\img\image-20200427145815491.png)

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

## 笔记

* [note1 ASP 和 VBScript](./note1)
* [note2 Request 和 Response](./note2)
* [note3 Cookie 和作用域](./note3)
* [note4 AJAX](./note4) 
* [sup1 Access 和 SQL](./sup1)
* [note5 ADO](./note5)

