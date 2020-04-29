# BootStrap

> BootStrap 网站：[BootStrap](https://getbootstrap.com/)

BootStrap 是一个前端组件库，帮助写更好看的页面。

## Layout

BS 使用网格来布局

```html
<div class="container">
  <div class="row">
    <div class="col-sm">
      One of three columns
    </div>
    <div class="col-sm">
      One of three columns
    </div>
    <div class="col-sm">
      One of three columns
    </div>
  </div>
</div>
```

列分成这几类


|                     | Extra small <576px                   | Small ≥576px | Medium ≥768px | Large ≥992px | Extra large ≥1200px |
| ------------------- | ------------------------------------ | ------------ | ------------- | ------------ | ------------------- |
| Max container width | None (auto)                          | 540px        | 720px         | 960px        | 1140px              |
| Class prefix        | `.col-`                              | `.col-sm-`   | `.col-md-`    | `.col-lg-`   | `.col-xl-`          |
| # of columns        | 12                                   |              |               |              |                     |
| Gutter width        | 30px (15px on each side of a column) |              |               |              |                     |
| Nestable            | Yes                                  |              |               |              |                     |
| Column ordering     | Yes                                  |              |               |              |                     |

可以用

```javascript
document.body.clientWidth;
document.body.clientHeight;
window.screen.height;
window.screen.width;
```

这两个 JavaScript 变量查看网页/屏幕的大小。

## Padding，Margin

首先，我们知道 `16px = 1rem` ，还知道 `margin` 决定元素和元素之间的距离，`padding` 决定元素和内容之间的距离。

在 BS 中，我们用 `{property}{sides}-{size}` 来写。

## Icon

### Font Awesome

[Font Awesome](https://fontawesome.com/)

### Feather Icons

[Feather Icons](https://feathericons.com/?query=eye)

```html
<script src="https://unpkg.com/feather-icons"></script>
<i data-feather="circle"></i>
<script>
    feather.replace()
</script>
```

## 其他资料

* [Flexbox 布局介绍](./flexbox)