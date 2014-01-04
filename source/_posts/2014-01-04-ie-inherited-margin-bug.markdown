---
layout: post
title: "IE inherited margin bug: form elements and hasLayout"
date: 2014-01-04 13:15
comments: true
categories: 哈喽！女汉纸
---
tags: `IE` `表单` `兼容`
<br>
总是要切换浏览器的“浏览器模式”和“文档模式”，来测试下IE浏览器是否显示正常，这两种模式的排列组合的情况总是搞不清相互有什么关系，先mark下——<br>
`浏览器模式`影响的是浏览器的版本及IE的条件注释，会影响服务器端对浏览器版本的判断,主要表现在展现，对CSS影响很大。<br>
`文档模式`影响的是IE的排版引擎，对DOM的渲染会产生影响。

hasLayout这个IE的特有属性已经很熟悉了，平常都是需要激发hasLayout来解决很多渲染的问题，这次遇到一个因为hasLayout=true造成的IE兼容性问题。<br>
问题代码演示：http://jsbin.com/oZeYOve/1/edit <br>
问题描述：input属性继承了父类的margin值，导致input左边的距离不受控制（事实上右边也会有问题）。也就是说input会继承父类水平方向的margin值，叠加到自身。IE7及以下浏览器会出现这个问题。

但是，出现该bug的前提是父类是一个被激活了hasLayout的元素。该例子中如果去掉div#search-box的width和height，问题可以被修复。或者将form元素包含到div#search-box元素内。但肯定要遇到“臣妾做不到啊”的情况。<br>
解决办法：<br>
1.CSS hack，给input设置margin负值，用来抵消继承下来的父类margin值。<br>
2.删除父类的margin值。<br>
3.取消父类的hasLayout属性。<br>
4.在input元素之前放文本元素，或者label元素，或者任何的行元素。<br>
5.用span元素把input包起来。

另外我其实遇到过另一个奇葩的问题，input的左边距坍塌。浏览器查看样式点来点去的时候，左边距生效，静止的时候，左边距又退回去了！因为项目中这个页面去掉了，也没办法重现，不知道是哪里的起了冲突。还是先mark

参考资料:[1][http://www.positioniseverything.net/explorer/inherited_margin.html](http://www.positioniseverything.net/explorer/inherited_margin.html)