---
layout: docs
title: 常见问题
prev_section: deployment-methods
next_section: sites
permalink: /docs/troubleshooting/
contributor: Youngv
---

如果你在安装或者使用 Jekyll 的过程中遇到了问题，这里有一些建议也许可以帮助到你。如果你所遇到的问题没有包含在下面，请[提交一个 issue]({{ site.repository }}/issues/new)，这样 Jekyll 团队才能让每个人有更好的使用体验。

## 安装问题
如果你在安装 gem 的过程中遇到问题，可能你需要安装为 ruby 1.9.1 的拓展模块编译所需要的头文件，在 Ubuntu 或 Debian 系统中安装可以通过运行：

{% highlight bash %}
sudo apt-get install ruby1.9.1-dev
{% endhighlight %}

在 Rdd Hat，CentOS 和 Fedora 系统中安装你可以通过运行：

{% highlight bash %}
sudo yum install ruby-devel
{% endhighlight %}

在 [NearlyFreeSpeech](http://nearlyfreespeech.net/) 中你需要在运行命令的时候添加下面的环境变量：

{% highlight bash %}
RB_USER_INSTALL=true gem install jekyll
{% endhighlight %}

在 OSX 系统中你可能需要升级 RubyGems：

{% highlight bash %}
sudo gem update --system
{% endhighlight %}

如果你还是遇到问题，你可能需要[使用 XCode 来安装命令行工具](http://www.zlu.me/blog/2012/02/21/install-native-ruby-gem-in-mountain-lion-preview/)

{% highlight bash %}
sudo gem install jekyll
{% endhighlight %}

在 Gentoo 上安装 RubyGems：

{% highlight bash %}
sudo emerge -av dev-ruby/rubygems
{% endhighlight %}

在 Windows 下你可能需要安装 [RubyInstaller
DevKit](http://wiki.github.com/oneclick/rubyinstaller/development-kit)。

## 运行 Jekyll 时的问题
在 Debian 或者 Ubuntu 系统中，你可能需要在 path 里添加 `/var/lib/gems/1.8/bin/` 来使
`jekyll` 命令可以在终端中执行。

## Base-URL 问题
如果你正在这样使用 base-url 选项：
{% highlight bash %}
jekyll serve --baseurl '/blog'
{% endhighlight %}

… 那么你需要在访问网页的时候使用：
{% highlight bash %}
http://localhost:4000/blog/index.html
{% endhighlight %}

这样访问会出现错误：
{% highlight bash %}
http://localhost:4000/blog
{% endhighlight %}

## 配置问题
冲突的配置设置的优先顺序如下：
1.  命令行标志
2.  配置文件设置
3.  默认配置

也就是说，默认配置会被 `_config.yml` 中指定的选项所覆盖，而在命令行中指定的参数配置会覆盖其它地方的配置。

## Markup 问题
Jekyll 所使用的不同的 Markup 引擎可能会有一些问题。下面的文件可能会帮助你如果你遇到类似的问题。

### Maruku

如果你的链接中有一些需要避免的的词，你需要这样写：

{% highlight text %}
![Alt text](http://yuml.me/diagram/class/[Project]->[Task])
{% endhighlight %}

如果你有一个空的标签，比如 `<script src="js.js"></script>`，Maruku 会将它转换成 `<script src="js.js" />`。 这将会在火狐或者其它浏览器中出现问题，而且[在 XHTML 中不推荐使用](http://www.w3.org/TR/xhtml1/#C_3)。一个简单的避免方法就是在起始标签和结束标签之间放一个空格。

### RedCloth

4.1.1 和更高的版本将不支持 notextile 标签。[这是一个已知的 bug](http://aaronqian.com/articles/2009/04/07/redcloth-ate-my-notextile.html)可能有希望在 4.2 版本中得到修复。你可以继续使用 4.1.9 版本，但是测试套件需要安装 4.1.0 版本。如果使用一个不支持 notextile 标签的版本， 你可能需要注意 Pygments 的语法高亮格式会不正确，还有其它一些可能的问题。如果你遇到这个问题你只需要安装 4.1.0 版本。

### Liquid

最新的 2.0 版本似乎打破了 `{{ "{{" }}` 在模板中的使用，不再类似以前的版本，在 2.0 版本使用 `{{ "{{" }}` 会出现以下问题：

{% highlight bash %}
'{{ "{{" }}' was not properly terminated with regexp: /\}\}/  (Liquid::SyntaxError)
{% endhighlight %}

### 摘要

从 V1.0.0 版本开始，Jekyll 已经可以自动生成文章摘要。 一直到 v1.1.0 版本，Jekyll 仍使用Liquid 来传递摘要，这将会在引用不存在或标记没有被关闭时造成奇怪的问题。如果你遇到了这些问题，你可以尝试将在 `_config.yml` 中设置 `excerpt_separator: ""` 或设置成不敏感的字符。

<div class="note">
  <h5>请为你遇到的问题提交一个 issue</h5>
  <p>如果你发现一个 bug，请在 GitHub 上<a href="{{ site.repository }}/issues/new">提交一个 issue</a> 描述你所遇到的问题和你的解决方案，我们就能把它放在这里帮助其它用户。</p>
</div>
