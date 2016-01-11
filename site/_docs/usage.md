---
layout: docs
title: 基本用法
permalink: /docs/usage/
translators: [Neo-J, chaucerling, archersmind]
hash: 5647b91
---

安装了 Jekyll 的 Gem 包之后，就可以在命令行中使用 Jekyll 命令了。有以下这些用法：

{% highlight bash %}
$ jekyll build
# => 当前文件夹中的内容将会生成到 ./_site 文件夹中。

$ jekyll build --destination <destination>
# => 当前文件夹中的内容将会生成到目标文件夹<destination>中。

$ jekyll build --source <source> --destination <destination>
# => 指定源文件夹<source>中的内容将会生成到目标文件夹<destination>中。

$ jekyll build --watch
# => 当前文件夹中的内容将会生成到 ./_site 文件夹中，
#    查看改变，并且自动再生成。
{% endhighlight %}

<div class="note info">
  <h5>在自动构建过程中对 _config.yml 的修改将不会被包含其中。</h5>
  <p>
    <code>_config.yml</code> 管理包含全局配置和变量定义在内的配置文件
    并且这些变量定义在执行时会被读取. 所有 <code>_config.yml</code> 中的改动
    在自动构建过程中，都不会被加载直到下一次执行开始。
  </p>
  <p>
    注意 <a href="../datafiles">Data Files</a> 在自动构建过程中会被包含和加载。
  </p>
</div>

<div class="note warning">
  <h5>Destination 文件夹会在站点建立时被清理</h5>
  <p>
    <code>&lt;destination&gt;</code> 的内容默认在站点建立时会被自动清理。不是你创建的文件和文件夹会被删除。你想在 <code>&lt;destination&gt;</code> 保留的文件和文件夹应在 <code>&lt;keep_files&gt;</code> 里指定。
  </p>
  <p>
    不要把<code>&lt;destination&gt;</code> 设置到重要的路径上，而应该把它作为一个暂存区域,从那里复制文件到您的web服务器。
  </p>
</div>

Jekyll 同时也集成了一个开发用的服务器，可以让你使用浏览器在本地进行预览。

{% highlight bash %}
$ jekyll serve
# => 一个开发服务器将会运行在 http://localhost:4000/
# Auto-regeneration（自动再生成文件）: 开启。使用 `--no-watch` 来关闭。

$ jekyll serve --detach
# => 功能和`jekyll serve`命令相同，但是会脱离终端在后台运行。
#    如果你想关闭服务器，可以使用`kill -9 1234`命令，"1234" 是进程号（PID）。
#    如果你找不到进程号，那么就用`ps aux | grep jekyll`命令来查看，然后关闭服务器。[更多](http://unixhelp.ed.ac.uk/shell/jobz5.html).
{% endhighlight %}


<div class="note info">
  <h5>知道默认行为</h5>
  <p>
    在2.4版本中， <code>serve</code> 指令将会自动监测变化。想关闭这功能，你可以使用 <code>jekyll serve --no-watch</code> ，这会保留旧行为。
  </p>
</div>

{% highlight bash %}
$ jekyll serve --no-watch
# => 和 `jekyll serve` 一样，但不会监测变化。
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

如果你对离线浏览这些文档感兴趣，可以安装 `jekyll-docs` 的 gem ，在你终端运行 `jekyll docs` 来查看。
