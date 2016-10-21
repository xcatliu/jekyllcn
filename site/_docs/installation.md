---
layout: docs
title: 安装
permalink: /docs/installation/
translators: [ Neo-J, xcatliu, TimoTokki, baiyangcao ]
update_date: 2016-10-20
hash: 5647b91
---

安装完成 Jekyll 需要几分钟的时间。如果你觉得安装对你来说并不方便, 请 [file an
issue]({{ site.repository }}/issues/new) (或者提交一个 pull request)
来描述一下你的遭遇并告诉我们如何使这个安装过程更加便捷。

### 事先准备

安装 Jekyll 相当简单，但是你得先做好一些准备工作。开始前你需要确保你在系统里已经有如下配置。

- [Ruby](http://www.ruby-lang.org/en/downloads/)（including development headers, Jekyll 2 需要 v1.9.3 及以上版本，Jekyll 3 需要 v2 及以上版本）
- [RubyGems](http://rubygems.org/pages/download)
- Linux, Un ix, or Mac OS X
- [NodeJS](http://nodejs.org), 或其他 JavaScript 运行环境（Jekyll 2 或更早版本需要 CoffeeScript 支持）。
- [Python 2.7](https://www.python.org/downloads/)（Jekyll 2 或更早版本）

<div class="note info">
  <h5>在 Windows 下使用 Jekyll</h5>
  <p>
    虽然官方不建议在 Windows 下运行，但你可以看看这个文档：
    <a href="../windows/#installation">Windows 环境文档</a>
  </p>
</div>

## 用 RubyGems 安装 Jekyll

安装 Jekyll 的最好方式就是使用
[RubyGems](http://rubygems.org/pages/download). 你只需要打开终端输入以下命令就可以安装了：

{% highlight bash %}
$ gem install jekyll
{% endhighlight %}

所有的 Jekyll 的 gem 依赖包都会被自动安装，所以你完全不用去担心。如果你在安装中碰到了问题，请查看 [troubleshooting](../troubleshooting/) 或者
[report an issue]({{ site.repository }}/issues/new) 那么 Jekyll 社区就会帮助你解决问题了。

<div class="note info">
  <h5>安装 Xcode Command-Line Tools</h5>
  <p>
    如果你是Mac用户，你就需要安装 Xcode 和 Command-Line Tools了。下载方式：
    <code>Preferences &#8594; Downloads &#8594; Components</code>。
  </p>
</div>

## 安装预览版

要安装 Jekyll 预览版，需要在完成事先准备之后运行：

{% highlight bash %}
gem install jekyll --pre
{% endhighlight %}

这将会安装最新版本的 Jekyll。如果你想安装指定版本，只需要加上 `-v` 参数即可：

{% highlight bash %}
gem install jekyll -v '2.0.0.alpha.1'
{% endhighlight %}

如果你想安装 Jekyll 开发版，那就有点复杂。你将会拥有最新的特性，但是也不稳定，安装方式如下：

{% highlight bash %}
$ git clone git://github.com/jekyll/jekyll.git
$ cd jekyll
$ script/bootstrap
$ bundle exec rake build
$ ls pkg/*.gem | head -n 1 | xargs gem install -l
{% endhighlight %}

## 附加功能

根据每个人使用方式的不同，Jekyll 还支持你安装一些附加功能。包括了对 LaTeX 的支持，以及使用动态内容渲染引擎。查看 [the extras page](../extras/) 获得更多信息。

<div class="note">
  <h5>ProTip™: 允许代码高亮</h5>
  <p>
    如果你是一个使用 Jekyll 的程序员，用 <a href="http://pygments.org/">Pygments</a>
    或者 <a href="https://github.com/jayferd/rouge">Rouge</a> 来支持代码高亮吧。当然，使用前请先查看
    <a href="../templates/#code_snippet_highlighting">文档</a>。
  </p>
</div>

## 已经安装老版本Jekyll？

在使用Jekyll开发之前，你可能想要检查一下你的Jekyll是不是最新版本，想要查看你的Jekyll版本，执行下面命令之一：

{% highlight bash %}
$ jekyll --version
$ gem list jekyll
{% endhighlight %}

你可以在[RubyGem](https://rubygems.org/gems/jekyll)找到任何gem软件包的最新版本，同时也可以通过`gem`命令行工具来查看：

{% highlight bash %}
$ gem search jekyll --remote
{% endhighlight %}

这样你会查到名为`jekyll`的gem包，并且在方括号中显示最新版本。另一个检查本机是否是最新版本的办法是执行命令`gem outdated`，
它会显示出当前系统中所有需要更新的gem包列表，如果你的jekyll不是最新版本，执行命令：

{% highlight bash %}
$ gem update jekyll
{% endhighlight %}

哦耶～你已经安装了所有需要的东西了，开始玩转 Jekyll 吧！
