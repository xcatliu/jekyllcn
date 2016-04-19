---
layout: docs
title: Windows 运行Jekyll
permalink: /docs/windows/
translators: comsince
---

虽然Windows并不是Jekyll官方支持的平台，但是也可以通过合适的方法使其运行在windows平台上。这个页面旨在收集一些由Windows用户发掘出来的关于Jekyll相关的知识和课程。

## 安装

JuLian Thilo 已经写出关于[Jekyll 运行于Windows上][windows-installation]的指南，并且看来试用于绝大数情况。这个说明是为Ruby 2.0.0 写的，但是应该也试用了之后的版本[2.2之前版本][hitimes-issue]

## 编码

如果你使用UTF-8编码，请确保你的问题见中不存在`BOM` 字符，否则ekyll将会出现意想不到的情况。特别是你要在Windows上使用Jekyll，这个问题就需要特别注意。
另外，你可能需要将代码控制台页面的编码修改为UTF-8,否则将会出现一个异常：在生成网页的时候，使用了不正确的编码。可以通过以下的命令解决：
{% highlight bash %}
$ chcp 65001
{% endhighlight %}

[window 安装]: http://jekyll-windows.juthilo.com/
[hitimes-issue]: https://github.com/copiousfreetime/hitimes/issues/40

## 自动-重构建

到1.3.0后，当`--watch`  开关在编译和运行是指定后，Jekyll 使用 gem 的`listen`去监听变化。然而`listen` 只支持基于UNIX的操作系统，在Windows上需要一个额外的gem才能与其兼容。将下面的命令加入你的站点的gemfile中。

{% highlight ruby %}
gem 'wdm', '~> 0.1.0' if Gem.win_platform?
{% endhighlight %}
