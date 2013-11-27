---
layout: docs
title: 升级
prev_section: resources
next_section: contributing
permalink: /docs/upgrading/
contributor: debbbbie
---

是时候该升级你的 Jekyll 了，升级之前为你介绍一下版本 1.0 的更新内容。

首先，我们需要获取 Jekyll 的最新版本：

{% highlight bash %}
$ gem update jekyll
{% endhighlight %}

<div class="note feature">
  <h5 markdown="1">提示</h5>
  <p markdown="1">想要迅速建立起一个 Jekyll 站点并跑起来吗？只需要输入命令
 <code>jekyll new SITENAME</code>，该命令将创建一个包含基本功能的 Jekyll 站点。</p>
</div>

### Jekyll 命令

Jekyll 现在支持命令 `build` 和 `serve`，使用起来更加清晰。
以前你或许会使用命令 `jekyll` 生成一个网站并用 `jekyll --server` 在本地浏览， 
现在可以用子命令 `jekyll build` 和 `jekyll serve` 代替。
如果当一个文件改变时，你希望 Jekyll 自动做出相应的更新，只需要在命令的末尾加上 `--watch` 即可。

<div class="note info">
  <h5>Watching 和 Serving</h5>
  <p markdown="1">使用新的子命令，网站的操作方式也有一些变化。以前的做法是在网站配置文件中加上
 `server: true`，现在用 `jekyll serve` 即可。 同样的 `watch: true` 也是如此，在
 `jekyll serve` 或 `jekyll build` 后边加上 即可 `&#45;&#45;watch`。</p>
</div>

### 绝对地址

在 Jekyll v1.0 中，我们引入了“绝对地址”。v1.1 之前，使用 **opt-in**。从 v1.1 开始, 
将使用 **opt-out** ，这意味着 Jekyll 将使用绝对地址代替相对相对地址。

* 如果要使用绝对地址，需要在配置文件中加上 `relative_permalinks: false` 。
* 如果要继续使用相对地址，在配置文件中加上 `relative_permalinks: true` 。

<div class="note warning" id="absolute-permalinks-warning">
  <h5 markdown="1">在 v1.1 中，绝对地址将成为默认配置</h5>
  <p markdown="1">
    从 Jekyll v1.1.0 开始， `relative_permalinks` 默认为 `false`，这意味着所
    有页面默认为绝对地址，该配置会一直保留到 v2.0 。
  </p>
</div>

### 草稿箱

Jekyll 现在支持草稿箱，并且可以很容易的在发布前预览。想要开始编写草稿，只需要在项目
中建立 `_drafts` 文件夹（和 `_posts` 在同一目录），然后新建一个 markdown 文件即可。
想要预览你的草稿，只需要在命令 `jekyll serve` 后边加上 `--drafts` 。

<div class="note info">
  <h5 markdown="1">草稿没有日期</h5>
  <p markdown="1">
    跟文章不同，草稿没有日期，因为还没有发布。只需用标题（比如 `my-draft-post.md` ）
    做为文件名，而不是 `2013-07-01-my-draft-post.md` 。</p>
</div>

### 自定义配置文件

不仅可以通过在命令行末加标志, 还能够使用一个 Jekyll 自定义配置文件。这样可以帮助区分不同
的环境，或以编程方式覆盖用户指定的配置。只需要在命令 `jekyll` 后加上 `--config` ，然后
输入一个或多个配置文件的路径（以逗点隔开，不能有空格）。

#### 所以，不再建议使用以下这些命令：

* `--no-server`
* `--no-auto`
* `--auto` (现在的 `--watch`)
* `--server`
* `--url=`
* `--maruku`，`--rdiscount` ，和 `--redcarpet`
* `--pygments`
* `--permalink=`
* `--paginate`

<div class="note info">
  <h5>显式指定配置文件</h5>
  <p markdown="1">如果你使用了标志 `&#45;&#45;config` ， Jekyll 将忽略文件
    `&#95;config.yml` 。想对个配多置文件中组合使用吗？没问题， Jekyll 支持通过命令行
    指定多个配置文件。越往右，配置文件优先级越高。如果我运行
    `jekyll serve &#45;&#45;config &#95;config.yml,&#95;config-dev.yml`，并且他们
    包含同一个配置项，那么这个配置项的结果将是右边 `&#95;config-dev.yml` 的值，而非
    左边`&#95;config.yml` 。</p>
</div>

### 新的配置选项

Jekyll 1.0 引进了几个新的配置选项. 在升级之前，你应该检查一下在 pre-1.0 的配置文件中是否
有这些，如果有，确保正确配置了：

* `excerpt_separator`
* `host`
* `include`
* `keep_files`
* `layouts`
* `show_drafts`
* `timezone`
* `url`

### 根路径

通常，你想要在不同的地方运行你的 Jekyll 站点，比如发布前在本地预览。Jekyll 1.0 中使用标志
 `--baseurl` 即可。要使用这个特写，首先在网站的 `_config.yml` 中写入生产环境的 `baseurl`
 ；然后，遍历一遍代码，对所有相对地址加上前缀 `{% raw %}{{ site.baseurl }}{% endraw %}`.
当你想在本地测试的时候，在 `jekyll serve` 后传入标志 `--baseurl` 并跟上本地地址即可
（可能是 `/` ）。


<div class="note warning">
  <h5 markdown="1">所有的地址包含斜杠</h5>
  <p markdown="1">如果你按照上边的方法做了，记得所有的地址前有一个斜杠。因此，
 `site.baseurl = /` 和 `post.url = /2013/06/05/my-fun-post/`最终形成的地址有两个斜杠
开头。所以建议在  `baseurl` 不是 `/`时使用  `site.baseurl`。</p>
</div>
