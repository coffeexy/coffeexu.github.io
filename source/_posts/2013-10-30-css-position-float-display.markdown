---
layout: post
title: "讲一讲CSS的position/float/display"
date: 2013-10-30 21:51
comments: true
categories: 哈喽！女汉纸
---
tags: `CSS` `position` `float` `display`
<br>

###position

1. position属性取值：static(默认)、relative、absolute、fixed、inherit。

2. postision：static；始终处于文档流给予的位置。看起来好像没有用，但它可以快速取消定位，让top，right，bottom，left的值失效。在切换的时候可以尝试这个方法。
3. 除了static值，在其他三个值的设置下，z-index才会起作用。（确切地说z-index只在定位元素上有效）
4. position：relative和absolute都可以用于定位，区别在于前者的div还属于正常的文档流，后者已经是脱离了正常文档流，不占据空间位置，不会将父类撑开。定位原点relative是相对于它在正常流中的默认位置偏移，它原本占据的空间任然保留；absolute相对于第一个position属性值不为static的父类。所以设置了position：absolute，其父类的该属性值要注意，而且overflow：hidden也不能乱设置，因为不属于正常文档流，不会占据父类的高度，也就不会有滚动条。
5. fixed旧版本IE不支持，却是很有用，定位原点相对于浏览器窗口，而且不能变。常用于header，footer，或者一些固定的悬浮div，随滚动条滚动又稳定又流畅，比JS好多了。fixed可以有很多创造性的布局和作用，兼容性是问题。
6. position：inherit。规定从父类继承position属性的值，所以这个属性也是有继承性的。

###float

1. float属性取值：none(默认)、left、right、inherit。
2. float：left(或right)，向左（或右）浮动，直到它的边缘碰到包含框或另一个浮动框为止。且脱离普通的文档流，会被正常文档流内的块框忽略。不占据空间，无法将父类元素撑开。
3. 任何元素都可以浮动，浮动元素会生成一个块级框，不论它本身是何种元素。因此，没有必要为浮动元素设置display：block。
4. 如果浮动非替换元素，则要指定一个明确的width，否则它们会尽可能的窄。（什么叫替换元素？根据元素本身的特点定义的， (X)HTML中的img、input、textarea、select、object都是替换元素，这些元素都没有实际的内容。 (X)HTML 的大多数元素是不可替换元素，他们将内容直接告诉浏览器，将其显示出来。）

####清浮

1. 最直接的clear属性，该属性表示的是框的哪边不应该挨着浮动框。这个属性是对元素本身而言，通过自动为该元素增加上外边距实现的（css1和css2），或者在上外边距之上增加清除空间，而外边距本身不改变的方式（css2.1）。clear的缺陷是可能要添加额外无意义的标签。
2. 通过父类的浮动也可以清理子类浮动，将空间撑开。这有点像负负得正。但原理应该是浮动的元素也是按照文档流的方式布局，只不过它们是另外一个独立的文档流，不同于普通文档流，暂时叫它浮动文档流？
3. hasLayout和BFC都可以清理浮动。overflow：hidden；zoom:1；hasLayout跟BFC不同之处，前者被限制为一个矩形，可以设置宽高，但BFC不一定可以设置宽高（比如行内元素）。

###display

1. display属性取值：none、inline、inline-block、block、table相关属性值、inherit以及list-item, run-in等
2. display属性规定元素应该生成的框的类型。文档内任何元素都是框，块框或行内框。
3. display：none和visiability：hidden都可以隐藏div，区别有点像absolute和relative，前者不占据文档的空间，后者还是占据文档的位置。
4. display：inline和block，又叫行内元素和块级元素。表现出来的区别就是block独占一行，在浏览器中通常垂直布局，可以用margin来控制块级元素之间的间距（存在margin合并的问题，就是@ 寒冬winter 磨叽的margin collapse么- -||，插一句， 只有普通文档流中块框的垂直外边距才会发生外边距合并。行内框、浮动框或绝对定位之间的外边距不会合并。）；而inline以水平方式布局，垂直方向的margin和padding都是无效的，大小跟内容一样，且无法设置宽高。inline就像塑料袋，内容怎么样，就长得怎么样；block就像盒子，有固定的宽和高。
5. inline-block就介于两者之间。inline-block行内块元素。内容被格式化为块元素，而元素本身是一个行内元素。可以设置宽高，又默认不换行特性。IE表现出来的效果不一样，所以需要激发hasLayout，所以就产生了这么一串代码{display:inline-block;*display:inline; *zoom:1;}。但是不一定要这么累赘，因为还有其他值也可以激发hasLayout，比如height/width。inline-block跟float可以达到同样的布局效果。效果哪个好不好说，前者不会打破文档正常的定位机制，后者就脱离了正常的文档流。完全看具体布局情况选择。另外，激发hasLayout之后的并且设置display：inline的元素，跟普通文字一样按水平方向排列，受vertical-align的影响，并且可以按照容器大小自适应调整。
6. table相关的属性值可以用来垂直居中，效果一般。

###定位机制


1. 上面三个属性都属于CSS定位属性。CSS三种基本的定位机制：普通流、浮动、绝对定位。

####随便扯一些居中布局：

* 宽高固定可以利用负margin。

```
.center{top：50%;margin-top:-height/2;left:50%;margin-left:-width/2;}
```

* 宽高不固定的元素。.center{display：inline-block},父类设置{text-align:center}

* 垂直居中table-cell不说了

* {line-height：height;vertical-align:middle;}

* {position:absolute;top:0;bottom:0;margin:auto}别忘记给父类定位{position:relative;}