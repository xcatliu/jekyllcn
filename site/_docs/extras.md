---
layout: docs
title: 附加功能
permalink: /docs/extras/
translators: [ikenbe, AlanTanis]
update_date: 2016-05-09
hash: 5647b91
---

根据你使用 Jekyll 的不同方式，Jekyll 允许你安装一些可选的附加功能。

## 数学支持

使用 Kramdown 时可以选择使用由 [MathJax](http://www.mathjax.org/) 提供的 LaTeX 格式到 PNG 格式的数学区块渲染器。具体细节可查阅 Kramdown 文档中的 [math blocks (数学区块)](http://kramdown.gettalong.org/syntax.html#math-blocks) 以及 [math support (数学支持)](http://kramdown.gettalong.org/converter/html.html#math-support) 部分。
使用 MathJax 需要你设置引用相关的 JavaScript 或 CSS 资源来渲染 LaTeX, 例如：
{% highlight html %}
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
{% endhighlight %}
若想获取更多入门信息，你可以参考这篇[极佳的文章](http://gastonsanchez.com/opinion/2014/02/16/Mathjax-with-jekyll/)。

## 使用其它 Markdown 解析器

关于如何使用其它的 Markdown 解析器，请参考 [configuration page (配置页面)](/docs/configuration/#markdown-options) 的 Markdown 部分；你也可以在 [custom processors (自定义解析器)](/docs/configuration/#custom-markdown-processors) 部分找到如何创建新的解析器。
