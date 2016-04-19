---
layout: docs
title: Windows 环境下的 Jekyll
permalink: /docs/windows/
---

虽然 Windows 平台不是官方支持的平台，不过可以通过适当的调整来运行Jekyll。此页面收集了已经被 Windows 用户发现的一些常见问题以供参考。

## 安装

Julian Thilo 已经写了一份适用于大多数人的说明来指导你如何 [在 Windows 上运行Jekyll][windows-installation] 。
这份说明写给 Ruby 2.0.0, 但是应该适用于 [2.2 之前][hitimes-issue] 的新版本。

## 编码

如果你使用 UTF-8 编码, 确保没有 `BOM` header characters 存在于你的文件中 ，否则你的Jekyll会有非常糟糕的事发生。 如果你要在 Windows 上运行 Jekyll 这点很关键。

另外, 你可能需要改变控制台窗口的代码页为 UTF-8 防止在站点生成的过程中出现 "Liquid Exception: Incompatible character encoding" 错误。 通过下面的命令完成：

{% highlight bash %}
$ chcp 65001
{% endhighlight %}

[windows-installation]: http://jekyll-windows.juthilo.com/
[hitimes-issue]: https://github.com/copiousfreetime/hitimes/issues/40

## 自动重建

自 v1.3.0 起, 在 build 或 serve 期间当 `--watch` switch 被指定时，Jekyll 使用 `listen` gem 来监视更改。 而 `listen` 已经内建支持 UNIX 系统, 它需要一个额外的 gem 来兼容 Windows. 为你的站点添加以下内容到 Gemfile ：

{% highlight ruby %}
gem 'wdm', '~> 0.1.0' if Gem.win_platform?
{% endhighlight %}
