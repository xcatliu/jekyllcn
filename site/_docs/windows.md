---
layout: docs
title: Windows 运行Jekyll
permalink: /docs/windows/
translators: [comsince, StromKuo, xcatliu] 
---

虽然 Windows 并不是 Jekyll 官方支持的平台，但是也可以通过合适的方法使其运行在 Windows 平台上。这个页面旨在收集一些由 Windows 用户发掘出来的关于 Jekyll 相关的知识和课程。

## 安装

JuLian Thilo 已经写出关于 [Jekyll 运行于Windows上][windows-installation] 的指南，并且看来试用于绝大数情况。这个说明是为 Ruby 2.0.0 写的，但是应该也试用了之后的版本 [2.2之前版本][hitimes-issue]

## 编码

如果你使用 UTF-8 编码，请确保你的问题见中不存在 `BOM` 字符，否则 Jekyll 将会出现意想不到的情况。特别是你要在 Windows 上使用 Jekyll，这个问题就需要特别注意。

另外，你可能需要将代码控制台页面的编码修改为 UTF-8，否则将会出现一个异常：在生成网页的时候，使用了不正确的编码。可以通过以下的命令解决：

{% highlight bash %}
$ chcp 65001
{% endhighlight %}

[window 安装]: http://jekyll-windows.juthilo.com/
[hitimes-issue]: https://github.com/copiousfreetime/hitimes/issues/40

## 自动-重构建

到 1.3.0 后，当 `--watch` 开关在编译和运行是指定后，Jekyll 使用 gem 的 `listen` 去监听变化。然而 `listen` 只支持基于 UNIX 的操作系统，在 Windows 上需要一个额外的 gem 才能与其兼容。将下面的命令加入你的站点的 gemfile 中。

{% highlight ruby %}
gem 'wdm', '~> 0.1.0' if Gem.win_platform?
{% endhighlight %}
