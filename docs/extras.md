---
layout: docs
title: 附加功能
prev_section: plugins
next_section: github-pages
permalink: /docs/extras/
contributor: yizeng
---

Jekyll 提供了诸多 (可任选) 的附加功能，你可以依据你使用 Jekyll 的需求来选择安装它们。

## LaTeX 支持

Maruku 自带了将 LaTeX 渲染成 PNG 的功能可供选择，此功能使用
blahtex (版本 0.6)，必须和 `dvips` 一起被置于你的 `$PATH` 中。
如果你需要 Maruku 不调用默认位置的 `dvips`，请查看
[Remi 的 Maruku fork](http://github.com/remi/maruku).

## RDiscount

如果你更喜欢使用 [RDiscount](http://github.com/rtomayko/rdiscount) 来替代
[Maruku](http://github.com/bhollis/maruku) 解析 Mardown，你只需确认已将其安装：

{% highlight bash %}
$ [sudo] gem install rdiscount
{% endhighlight %}

然后在你的 `_config.yml` 文件内选择 RDiscount 作为 Markdown 引擎，使 Jekyl 可以读取该选项来运行。

{% highlight yaml %}
# _config.yml 中
markdown: rdiscount
{% endhighlight %}

## Kramdown

你还可以选择 [Kramdown](http://kramdown.rubyforge.org/) 来替代
Maruku 解析 Mardown，你只需确认 Kramdown 已被安装：

{% highlight bash %}
$ [sudo] gem install kramdown
{% endhighlight %}

然后在你的 `_config.yml` 文件内选择 Kramdown 作为 Markdown 引擎。

{% highlight yaml %}
# _config.yml 中
markdown: kramdown
{% endhighlight %}

Kramdown 提供了各种选项用来自定义其 HTML 的输出。
[配置](/docs/configuration/)页面列出了
Jekyll 所使用的默认选项。一份完整的选项列表也可见于
[Kramdown 网站](http://kramdown.rubyforge.org/options.html)。
