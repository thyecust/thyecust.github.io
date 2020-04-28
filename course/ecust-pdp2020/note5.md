# 程序设计实践 5：ADO

> 课程：[程序设计实践 2020 春](./index)
>
> 例子使用 Access，请看 [补充 1：Access 和 SQL](./sup1)

ADO 是 ActiveX Data Objects 的缩写，使 ASP 可以与数据库交互。

一个 ASP 页面与数据库交互的过程是

1. 建立 ADO 连接
2. 打开一个数据库
3. 创建一个 ADO recordset
4. 打开 recordset
5. 从 recordset 获取需要的数据
6. 关闭 recordset
7. 关闭 ADO 连接

## Hello ADO

一个例子

```asp
<%
    set conn = Server.CreateObject("ADODB.Connection")
    conn.Provider="Microsoft.Jet.OLEDB.4.0"
    conn.Open("C:\Users\tianh\Documents\ecust\zhai-lab\pdp2020.mdb")
    set rs=Server.CreateObject("ADODB.Recordset")
    rs.Open "Student", conn
%>
<table>
    <tr>
        <th>学号</th>
        <th>姓名</th>
        <th>年龄</th>
    </tr>
    <% do while not rs.EoF %>
    <tr>
        <td><% = rs("SID") %></td>
        <td><% = rs("SName") %></td>
        <td><% = rs("SAge") %></td>
    </tr>
    <% rs.movenext %>
    <% loop %>
</table>
<%
	rs.close
	conn.close
%>
```

结果：

```html
<table>
    <tr>
        <th>学号</th>
        <th>姓名</th>
        <th>年龄</th>
    </tr>

    <tr>
        <td>1</td>
        <td>田昊宇</td>
        <td>19</td>
    </tr>

    <tr>
        <td>2</td>
        <td>Song Zheyi</td>
        <td>20</td>
    </tr>

    <tr>
        <td>3</td>
        <td>Han Meimei</td>
        <td>22</td>
    </tr>
</table>
```

## Recordset

上面的例子中，`conn` 是一个数据库连接对象，`rs` 是一个 Recordset 对象，我们的 CRUD 都是通过 `rs` 进行的

```vbscript
set conn = Server.CreateObject("ADODB.Connection")
conn.Provider="Microsoft.Jet.OLEDB.4.0"
conn.Open("C:\Users\tianh\Documents\ecust\zhai-lab\pdp2020.mdb")
set rs=Server.CreateObject("ADODB.Recordset")
rs.Open "Student", conn
```

### 创建

除了这样用表的名字创建，也可以用 SQL 语句创建，如

```vbscript
set rs=Server.CreateObject("ADODB.Recordset")
rs.Open "SELECT * FROM Student", conn
```

也可以用 `conn.Execute()` 创建，如

```vbscript
set rs = conn.Execute("SELECT * FROM Student")
```

### 读取数据

像最开始的例子一样，可以直接用字段名读取数据

```vbscript
rs('SName')
```

另外，可以用 `rs.fields` 读取数据，如

```vbscript
set rs = conn.Execute("SElECT * FROM Student")
for each x in rs.fields
	response.write(x.name)
    response.write(" = ")
    response.write(x.value & "<br/>")
next
```

的结果是

```html
SID = 1<br/>SName = 田昊宇<br/>SSex = True<br/>SAge = 19<br/>
```

可见，`rs.fields` 是一个列表，列表里的每一个元素都有两个属性

* `rs.fields(0).name` ，字段名
* `rs.fields(0).value`，该字段的值

而要读取下一条记录，就需要 `rs.movenext` 

```vbscript
set rs = conn.execute("SElECT * FROM Student")
rs.movenext
for each x in rs.fields
    response.write(x.name)
    response.write(" = ")
    response.write(x.value&"<br/>")
next
```

的结果是

```html
SID = 2<br/>SName = Song Zheyi<br/>SSex = True<br/>SAge = 20<br/>
```

我们怎么知道已经到了数据表的最后一条记录呢？`rs` 有一个属性 `rs.EOF` ，读到最后一条记录之前一直是 `false`，读到最后一条记录的时候还是 `false`，但是再往后一位就变成 `true`。当 `rs.EOF` 为 `true` 的时候，`rs.fields` 和 `rs.movenext` 都会报错。

另外，`rs` 有一个方法 `rs.GetString()` 

```vbscript
str = rs.GetString(format,rows,coldel,rowdel,nullexpr)
```

这样就可以避免 do loop，执行速度更快，例如最开始的例子就可以写出

```asp
str = rs.GetString(,,"</td><td>","</td></tr><tr><td>","&nbsp;")
response.write("<td>" & str & "</td>")
```

这样列和列之间自动填 `</td><td>`，行和行之间自动填 `</td></tr><tr><td>`，空的值自动写成 `&nbsp;` 。

### 增加/删除/修改数据

比如要 ASP 页面要往数据库新加一个数据，只需要

```vbscript
sql = "INSERT INTO Student(SNname) VALUES ("Li Ming")"
conn.execute(sql)
```

增加和修改也可以这么写，但是很明显，这种方式不能避免 SQL 注入式攻击。

另外，因为 SQL 语句可能执行失败所以报错，推荐这么写

```vbscript
sql = "..."
on error resume next
conn.execute sql
if err<>0 then
    response.write("No update permissions")
else
    response.write("Record ... was updated")
end if
```



