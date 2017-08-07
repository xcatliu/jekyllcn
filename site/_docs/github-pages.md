---
layout: docs
title: GitHub Pages
permalink: /docs/github-pages/
translators: [brickgao, archersmind, ydcool, baiyangcao]
update_date: 2016-10-21
---

[Github Pages](http://pages.github.com) 是面向用户、组织和项目开放的公共静态页面搭建托管服
务，站点可以被免费托管在 Github 上，你可以选择使用 Github Pages 默
认提供的域名 [github.io]() 或者自定义域名来发布站点。Github Pages 支持
自动利用 Jekyll 生成站点，也同样支持纯 HTML 文档，将你的 Jekyll 站
点托管在 Github Pages 上是一个不错的选择。

还没用过 Github Pages 制作网站?[通过 Jonathan McGlone 写的这篇奇妙的指南来创建和运行 Github Pages](http://jmcglone.com/guides/github-pages/)
这篇指南将告诉你关于 Git, GitHub 和 Jekyll 的相关知识，来建立一个属于你自己的站点。

### 项目站点的网址结构

你最好在将 Jekyll 站点提交到 `gh-pages` 之前先预览一下。因为 Github
上项目站点的子目录结构会使站点的网址结构变得复杂。为了正确构建站点，你的链接应该是这样的形式：`site.github.url`。

```xml
{% highlight html %}
{% raw %}
<!-- 用于静态名称的样式表... -->
<link href="{{ site.github.url }}/path/to/css.css" rel="stylesheet">
<!-- 用于动态URL的文档、页面... -->
<a href="{{ page.url | prepend: site.github.url }}">{{ page.title }}</a>
{% endraw %}
{% endhighlight %}
```


用这种方法你就可以在本地从根地址预览站点，而在 Github 上以 
`gh-pages` 分支生成站点的时候能以 `/project-name` 为根地址并且正确地
显示。

## 将 Jekyll 部署到 Github Pages 上

Github Pages 依靠 Github 上项目的某些特定分支来工作。Github Pages
分为两种基本类型：用户/组织的站点和项目的站点。搭建这两种类型站
点的方法除了一些小细节之外基本一致。


<div class="note protip">
  <h5>使用 <code>github-pages</code> gem包</h5>
  <p>
    我们在Github的朋友提供了
    <a href="https://github.com/github/pages-gem">github-pages</a>
    gem包来管理Jekyll和其在Github Pages上的依赖。使用这个包可以让你在将网站部署到Github Pages上时，
    不会因为各种不同版本的gem包而导致意外报错。想要在你的项目中使用当前部署版本的gem包，
    在你的 <code>Gemfile</code> 中添加如下内容：  

{% highlight ruby %}
{% raw %}
source 'https://rubygems.org'

require 'json'
require 'open-uri'
versions = JSON.parse(open('https://pages.github.com/versions.json').read)

gem 'github-pages', versions['github-pages']
{% endraw %}
{% endhighlight %}

    这回保证你再运行 <code>bundle install</code> 命令时，
    你能够安装正确版本的 <code>github-pages</code> gem包。

    如果执行失败，将上述内容简化为：

{% highlight ruby %}
{% raw %}
source 'https://rubygems.org'

gem 'github-pages'
{% endraw %}
{% endhighlight %}

    不过你要经常执行 <code>bundle update</code> 命令哦~~

    如果你想要在 Windows 上安装 <code>pages-gem</code> ，你可以参考 Jens Willmer 的这篇博文 <a href="http://jwillmer.de/blog/tutorial/how-to-install-jekyll-and-pages-gem-on-windows-10-x46#github-pages-and-plugins">how to install github-pages gem on Windows (x64)</a>。
  </p>
</div>

<div class="note info">
  <h5>在Windows上安装 <code>github-pages</code> gem包</h5>
  <p>
    尽管官方并不支持 Windows 系统，但还是可以在 Windows 系统上安装 <code>github-pages</code>滴！
    可以在我们提供的 <a href="../windows/#installation">Windows-specific docs page</a> 中找到一些参考。
  </p>
</div>

### 用户和组织的站点

用户和组织的站点被放置在一个特殊的专用仓库中，在该仓库中只存在
Github Pages 的相关文件。这个仓库应该根据用户/组织的名称来命名，
例如： [@mojombo 的用户站点仓库](https://github.com/mojombo/mojombo.github.io) 应该被命名为 `mojombo.github.io` 。

仓库中`master`分支里的文件将会被用来生成 Github Pages 站点，所以请
确保你的文件储存在该分支上。

<div class="note info">
  <h5>自定义域名不影响仓库命名</h5>
  <p>
    Github Pages 初始被设置部署在 
    <code>username.github.io</code> 子域名上, 这就是为什么
    <strong>即使你使用自定义域名</strong>仓库还需要这样命名。
  </p>
</div>

### 项目的站点

不同于用户和组织的站点，项目的站点文件存放在项目本身仓库的
`gh-pages` 分支中。该分支下的文件将会被 Jekyll 处理，生成的站点会被
部署到你的用户站点的子目录上，例如 `username.github.io/project` （除
非指定了一个自定义的域名）。

Jekyll 项目本身就是一个很好的例子，Jekyll 项目的代码存放在
[master 分支]({{ site.repository }}) ， 而 Jekyll 的项目站点（就是你现在看见的网页）包含在同一仓库的 
[gh-pages 分支]({{ site.repository }}/tree/gh-pages) 中。

<div class="note warning">
  <h5>源文件必须在根目录</h5>
  <p>
GitHub Pages <a href="https://help.github.com/articles/troubleshooting-github-pages-build-failures#source-setting">重载</a> 了 <a href="/docs/configuration/#global-configuration">“Site Source”</a> 配置的默认值，所以如果你将文件放在除了根目录之外的任何位置，都可能导致网站不能正确构建。
  </p>
</div>

<div class="note">
  <h5>GitHub Pages 文档，帮助和支持</h5>
  <p>
    关于 Github Pages 用法的更多相关信息，以及相关问题处理，你可以查看 <a
    href="https://help.github.com/categories/github-pages-basics/">GitHub’s Pages 帮助
    section</a>. 如果找不到相关内容，你可以联系 <a href="https://github.com/contact">GitHub Support</a>.
  </p>
</div>

