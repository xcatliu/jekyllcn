---
layout: docs
title: 基本用法
prev_section: installation
next_section: structure
permalink: /docs/usage/
contributor: Neo-J
---

安装了 Jekyll 的 Gem 包之后，就可以在命令行中使用 Jekyll 命令了。有以下这些用法：

{% highlight bash %}
$ jekyll build
# => 当前文件夹中的内容将会生成到 ./site 文件夹中。

$ jekyll build --destination <destination>
# => 当前文件夹中的内容将会生成到目标文件夹<destination>中。

$ jekyll build --source <source> --destination <destination>
# => 指定源文件夹<source>中的内容将会生成到目标文件夹<destination>中。

$ jekyll build --watch
# => 当前文件夹中的内容将会生成到 ./site 文件夹中，
#    查看改变，并且自动再生成。
{% endhighlight %}

Jekyll 同时也集成了一个开发用的服务器，可以让你使用浏览器在本地进行预览。

{% highlight bash %}
$ jekyll serve
# => 一个开发服务器将会运行在 http://localhost:4000/

$ jekyll serve --detach
# => 功能和`jekyll serve`命令相同，但是会脱离终端在后台运行。
#    如果你想关闭服务器，可以使用`kill -9 1234`命令，"1234" 是进程号（PID）。
#    如果你找不到进程号，那么就用`ps aux | grep jekyll`命令来查看，然后关闭服务器。[更多](http://unixhelp.ed.ac.uk/shell/jobz5.html).

$ jekyll serve --watch
# => 和`jekyll serve`相同，但是会查看变更并且自动再生成。
{% endhighlight %}

还有一些可以配置的[配置选项](../configuration/).
很多配置选项既可以在命令行中作为标识(flags)设定，也可以在源文件根目录中的 `_config.yml` 文件中进行设定。Jekyll 会自动加载这些配置。比如你在你的 `_config.yml` 文件中添加了下面几行：

{% highlight yaml %}
source:      _source
destination: _deploy
{% endhighlight %}

那么就等价于执行了以下两条命令：

{% highlight bash %}
$ jekyll build
$ jekyll build --source _source --destination _deploy
{% endhighlight %}

有关配置选项的更详细说明，请查看[配置](../configuration/)页面.
