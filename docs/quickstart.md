---
layout: docs
title: 快速指南
prev_section: home
next_section: installation
permalink: /docs/quickstart/
contributor: brickgao
---

以下是一个获取最简单 Jekyll 模板并生成静态页面的方法。

{% highlight bash %}
~ $ gem install jekyll
~ $ jekyll new myblog
~ $ cd myblog
~/myblog $ jekyll serve
# => Now browse to http://localhost:4000
{% endhighlight %}

就是这么简单。从现在开始，你可以通过创建文章、改变头信息来控制模板和输出、修改 Jekyll 设置来使你的站点变得更有趣～

<div class="note info">
  <h5>新站点的默认 Markdown 引擎是 Redcarpet</h5>
  <p>在 Jekyll 1.1 中，我们改变了默认的 Markdown 引擎，对于<code>jekyll new</code>产生的新站点，引擎将采用 Redcarpet。</p>
</div>

安装过程中有问题？去看看[安装](/docs/installation/)页面。
