---
layout: post
title: "外边距合并的其中一种"
date: 2013-10-21 20:31
comments: true
categories: 哈喽！女汉纸
---
tags: `外边距合并` `collapsing margins`
<br>
群里的一位同学遇到的问题：[JSBin](http://jsbin.com/OdEyoh/3/edit)

原本是一个居中的问题，为什么position修改为`relative`就不能居中了呢？

因为这里莫名其妙地满足了外边距合并的情况：

* 普通文档流的块级元素；

* 且一个元素包含在另一个元素中，没有`内边距`或`边框`把外边距分隔开。所以它们的上和/或下外边距发生了合并。所以麻烦都转移到父元素a上了。

解决办法：

* 使其中一个元素，变为`非`普通文档流中的块级元素，例如变为浮动元素(float)｜脱离文档流(position)｜内联元素(inline-block);
* 设置padding和border分开两个元素的外边距。(父元素上设置。子元素设置，还是没有把两个的margin分开好嘛)
* 父元素添加`overflow:hidden;`

一定要拜读的资料[w3school-CSS 外边距合并](http://www.w3school.com.cn/css/css_margin_collapsing.asp)
