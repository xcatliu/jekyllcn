---
layout: docs
title: 安装
prev_section: quickstart
next_section: usage
permalink: /docs/installation/
contributor: Neo-J
---
安装完成 Jekyll 需要几分钟的时间。如果你觉得安装对你来说并不方便, 请 [file an
issue]({{ site.repository }}/issues/new) (或者提交一个 pull request)
来描述一下你的遭遇并告诉我们如何使这个安装过程更加便捷。

### 事先准备

安装 Jekyll 相当简单，但是你得先做好一些准备工作
开始前你需要确保你在系统里已经有如下配置。

- [Ruby](http://www.ruby-lang.org/en/downloads/)
- [RubyGems](http://rubygems.org/pages/download)
- Linux, Unix, or Mac OS X

<div class="note info">
  <h5>在 Windows 下使用 Jekyll</h5>
  <p>
    你可以使用
    <a href="http://www.madhur.co.in/blog/2011/09/01/runningjekyllwindows.html">
    Jekyll running on Windows</a>, 但是官方文档并不建议你在 Windows 平台上安装 Jekyll。
  </p>
</div>

## 借助 RubyGems 安装 Jekyll

安装 Jekyll 的最好方式就是使用
[RubyGems](http://docs.rubygems.org/read/chapter/3). 你只需要打开终端输入以下命令就可以安装了：

{% highlight bash %}
$ gem install jekyll
{% endhighlight %}

所有的 Jekyll 的 gem 依赖包都会被自动安装，所以你完全不用去担心。如果你在安装中碰到了问题，请查看 [troubleshooting](../troubleshooting/) 或者
[report an issue]({{ site.repository }}/issues/new) 那么Jekyll社区就会帮助你和其他用户解决问题了。

<div class="note info">
  <h5>安装 Xcode Command-Line Tools</h5>
  <p>
    如果你是Mac用户，你就需要安装 Xcode 和 Command-Line Tools了。下载方式
    <code>Preferences &#8594; Downloads &#8594; Components</code>。
  </p>
</div>

## 附加功能

根据每个人使用方式的不同，Jekyll 还支持你安装一些附加功能。包括了对 LaTex 的支持，以及使用动态内容渲染引擎。
查看 [the extras page](../extras/) 获得更多信息。

<div class="note">
  <h5>ProTip™: 允许代码高亮</h5>
  <p>
    如果你是一个使用 Jekyll 的程序猿，用 Pygments 来支持代码高亮吧。当然，使用前请先查看
    <a href="../templates/#code_snippet_highlighting">how to do
    that</a>。
  </p>
</div>

哦耶～你已经安装了所有需要的东西了，开始玩转 Jekyll 博客吧！
