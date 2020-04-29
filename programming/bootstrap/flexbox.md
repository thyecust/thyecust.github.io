---
typora-copy-images-to: img
---

# Flexbox 布局

> 原文地址：[Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/#flexbox-background)

Flexbox 布局是为了解决“尺寸会变化的”元素的布局问题被发明的。

## 基础

Flexbox 不是一个标签或者属性，而是很多的属性，它涉及两个东西：容器（container）和容器里的东西（item）。

<img src=".\img\00-basic-terminology.svg" alt="A diagram explaining flexbox terminology. The size across the main axis of flexbox is called the main size, the other direction is the cross size. Those sizes have a main start, main end, cross start, and cross end."  />

基本概念

* main axis，也就是 item 排列的方向，由 `flex-direction` 属性定义
* main start，main end，item 排列的出发方向和终止方向
* main size，height 或 width，根据 main axis 的方向确定
* cross axis，垂直于 main axis 的方向
* cross start，cross end
* cross size

## 属性

### container

```css
.container{
    display: flex
}
```

`flex-direction`

<img src=".\img\image-20200428200254826.png" alt="image-20200428200254826" style="zoom: 50%;" />

```css
flex-direction: row | row-reverse | column | column-reverse;
```

`flex-wrap`

<img src=".\img\image-20200428200344080.png" alt="image-20200428200344080" style="zoom: 50%;" />

```css
flex-wrap: nowrap | wrap | wrap-reverse;
```

`justify-content`

<img src=".\img\image-20200428200450115.png" alt="image-20200428200450115" style="zoom:50%;" />

```css
justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly | start | end | left | right ... + safe | unsafe;
```

`align-items`

<img src=".\img\image-20200428200553002.png" alt="image-20200428200553002" style="zoom:50%;" />

```css
align-items: stretch | flex-start | flex-end | center | baseline | first baseline | last baseline | start | end | self-start | self-end + ... safe | unsafe;
```

`align-content`

<img src=".\img\image-20200428200847485.png" alt="image-20200428200847485" style="zoom:50%;" />

```css
align-content: flex-start | flex-end | center | space-between | space-around | space-evenly | stretch | start | end | baseline | first baseline | last baseline + ... safe | unsafe;
```

### item

`order`，一个数字，这个 item 出现的顺序，默认是 0。

`flex-grow`，一个正数，这个 item 可以在 main axis 可以最大占多大的份额，默认是 1。

`flex-shrink`，一个正数，这个 item 最小可以占多大的份额，默认是 1。



