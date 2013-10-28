---
layout: docs
title: 快速指南
permalink: /docs/quickstart/
category: docs
tags: getting-started
---

快速指南
========

以下是一个获取最简单Jekyll模板并生成静态页面的方法。

{% highlight bash %}
~ $ gem install jekyll
~ $ jekyll new myblog
~ $ cd myblog
~/myblog $ jekyll serve
# => Now browse to http://localhost:4000
{% endhighlight %}

就是这么简单。从现在开始，你可以通过创建文章、改变头信息来控制模板和输出、修改jekyll设置来使你的站点变得更有趣～

{% include note-open.html type="info" %}
##### 新站点的默认Markdown引擎是Redcarpet
在Jekyll 1.1中，我们改变了默认的Markdown引擎，对于`jekyll new`产生的新站点，引擎将采用Redcarpet。
{% include note-close.html %}

安装过程中有问题？去看看[安装](/docs/installation/)页面。
