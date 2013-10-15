---
layout: post
title: "Hello Again!Octopress"
date: 2013-10-10 20:45
comments: true
categories: 哈喽！女汉纸
---
tags: `折腾` `octopress`
<br>
这是第一次在mac上折腾Octopress, 对于我这种数码/IT杀手来说， 跟win一样麻烦。

但成就感暴涨。尤其是[茂茂](http://summer222522.github.io/)赞助了各种美好的[主题](https://github.com/imathis/octopress)后，更加激动兴奋了！！

哈哈，最喜欢折腾了！`折腾无止境`！

但是折腾完之后，不知道可以坚持纪录多久的博客，求监督。



接下来， 正式总结此次折腾遇到的麻烦。



### 坑

* 安装ruby——鉴于我手欠，早先删除了1个多G的Xcode，整个安装过程异常困难。由于我一直想要尝试用[戳工具](https://github.com/kennethreitz/osx-gcc-installer)来代替这个鸡肋的Xcode。毕竟，任何无用却占据大量空间的东西都使我感到无比难过。我觉得哪天`猴年马月`一定要替换过来。

```
	curl -L https://get.rvm.io | bash -s stable --ruby
	rvm install 1.9.3
	rvm use 1.9.3
	rvm rubygems latest
```

* 安装Octopress——安装依赖时，`rbenv rehash`总是提示没有这个命令。所以安装依赖的过程重复了好几次。最后`重启`，开`GoAgentX`，成功了。至于哪个原因造成的，我也不十分明了，有同样问题的可以参考[Mac上安装octopress](http://liuyix.org/blog/2013/mac-install-octopress/)。

```
	git clone git://github.com/imathis/octopress.git octopress
	cd octopress    # If you use RVM, You'll be asked if you trust the .rvmrc file (say yes).
	ruby --version  # Should report Ruby 1.9.3
	gem install bundler
	rbenv rehash    # If you use rbenv, rehash to be able to run the bundle command
	bundle install
	rake install
```


* 将博客部署到GitHub上——像我这种MAC小白，以为在终端输入代码，没有红色就算是成功，第一步执行完居然默默地隐藏着设置用户名和邮箱，就是github帐户的用户名和密码。这里要提示一下，目前github已经修改为`username.github.io`，写`.com`有什么问题呢？因为输入url的提示已经更新了，我一开始仓库名写的是`coffeexu.girhub.com`，提示里是
```
	git@github.com:CoffeeXu/coffeexu.github.io.git
	or https://github.com/username/username.github.io.git
```
显然我个猪头一来没粘贴仓库右下角的URL码，二来直接就将用户名改成了自己的名字。所以一直提示没有这个仓库。

如果使用的是ssh形式的url，需要得到当前笔记本用户的ssh，好像上面配置的时候会自动生产，如果需要手动添加的，戳[Generating SSH Keys](https://help.github.com/articles/generating-ssh-keys)。

```
	rake setup_github_pages
	rake generate
	rake deploy
```
不知道你们是怎么样，反正我的`rake deploy`是没有提交到github上，大概是我前面重复太多遍了，一直提示有冲突。肿么办呢？强制合并，手动提交。
```
	cd _deploy
	git add .
	git commit -m '手动提交_deploy'
	git push origin master
```

### DIY

* `rake preview`如果木有在线的markdown预览的话，这个是写文章和修改主题时好方法啊，开起来之后，即时修改即时刷新就可以预览效果。
* 超链接。有没有发现我文章内的连接是打开新窗口的呢，markdown目前应该还不支持这种语法的，当然markdown是支持html。来自己动动手操作下。[戳](https://gist.github.com/azone/4523641)
* 目前的主题，自然是自己做过修改啦！自己动手，丰衣足食。哈哈。设置css样式基本在`sass/parts`目录下
* 文本上下间距。嫌弃默认的间距实在是太大了，改了下。文件同上
* 本来添加了加网和友言的评论，觉得太山寨了，档次一下就low了，删掉了。目前使用的addthis的分享和多说的评论。addthis不能分享到微信，缺陷。所以可能还是尽量使用国内的玩意儿更加符合国情吧。
* tips.可以的话还是尽量看官方文档。当然最方便的就是——不要搞了啊！！！





