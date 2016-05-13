---
layout: docs
title: 快速指南
permalink: /docs/quickstart/
translators: [brickgao, chaucerling, TimoTokki]
update_date: 2016-04-19
hash: 5647b91
---

以下是一个获取最简单 Jekyll 模板并生成静态页面并运行的例子。

{% highlight bash %}
~ $ gem install jekyll
~ $ jekyll new myblog
~ $ cd myblog
~/myblog $ jekyll serve
# => Now browse to http://localhost:4000
{% endhighlight %}

如果你希望把 jekyll 安装到当前目录，你可以运行 `jekyll new .` 来代替。如果当前目录非空，你还需要增添 `--force` 参数，所以命令应为 `jekyll new . --force`。

就是这么简单。从现在开始，你可以通过创建文章、改变头信息来控制模板和输出、修改 Jekyll 设置来使你的站点变得更有趣～

安装过程中有问题？去看看[安装](/docs/installation/)页面。
