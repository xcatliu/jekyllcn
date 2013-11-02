---
layout: docs
title: GitHub Pages
prev_section: extras
next_section: deployment-methods
permalink: /docs/github-pages/
contributor: brickgao
---

[Github Pages](http://pages.github.com) 是面向用户、组织和项目开放的公共静态页面搭建托管服
务，站点可以被免费托管在 Github 上，你可以选择使用 Github Pages 默
认提供的域名 [github.io]() 或者自定义域名来发布站点。Github Pages 支持
自动利用 Jekyll 生成站点，也同样支持纯 HTML 文档，将你的 Jekyll 站
点托管在 Github Pages 上是一个不错的选择。

## 将 Jekyll 部署到 Github Pages 上

Github Pages 依靠 Github 上项目的某些特定分支来工作。Github Pages
分为两种基本类型：用户/组织的站点和项目的站点。搭建这两种类型站
点的方法除了一小些细节之外基本一致。

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

### 项目站点的网址结构

你最好在将 Jekyll 站点提交到 `gh-pages` 之前先预览一下。因为 Github
上项目站点的子目录结构会使站点的网址结构变得复杂。这里有一些处
理 Github Pages 子目录结构（`username.github.io/project-name/`）的方法
使你本地浏览的站点和部署在 Github Pages 上的站点一致，方便你的维
护。

1.  在 `_config.yml` 中，设置 `baseurl` 选项为 `/project-name` -- 注意必须存在头部的斜杠以及**不能**有尾部的斜杠。
2.  JS 或者 CSS 文件的引用格式应该如下：`{% raw %}{{ site.baseurl}}/path/to/css.css{% endraw %}` -- 注意斜杠之后必须紧随变量（在 "Path" 之后）。
3.  创建固定链接和内部链接的格式应该如下： `{% raw %}{{ site.baseurl }}{{ post.url }}{% endraw %}` -- 注意两个变量之间不存在斜杠。
4.  最后，如果你想在提交/部署之前浏览的话，请使用 `jekyll serve --baseurl ''`命令，请确定在 `--baseurl` 的选项之后存在**空串**，这样的话你就可以在 `localhost:4000` 看到你的站点（站点根地址不存在 `/project-name`）。

用这种方法你就可以在本地从根地址预览站点，而在 Github 上以 
`gh-pages` 分支生成站点的时候能以 `/project-name` 为根地址并且正确地
显示。

<div class="note">
  <h5>GitHub Pages 的文档，帮助和支持</h5>
  <p>
    想获得关于 Github Pages 的更多信息和解决方案，你应该访问
    <a href="https://help.github.com/categories/20/articles">GitHub’s Pages 帮助部分</a>。
    如果无法找到解决方案，你可以联系 <a
    href="https://github.com/contact">GitHub 支持</a>。
  </p>
</div>

### 模仿 Github 风格 Markdown
Github 风格 Markdown 与常规 Markdown 有
[些许差异](https://help.github.com/articles/github-flavored-markdown)。你可以在本地用
以下的[设置]({{ site.url }}/docs/configuration)
来模仿 Github 风格 Markdown。

{% highlight yaml %}
pygments: true
markdown: redcarpet
redcarpet:
  extensions:
    - hard_wrap
    - no_intra_emphasis
    - autolink
    - strikethrough
    - fenced_code_blocks
{% endhighlight %}

这些设置将为 Markdown 引擎引入以下来自 Github 风格 Markdown 的特性：

*   [换行](https://help.github.com/articles/github-flavored-markdown#newlines)
*   [语句中的多个下划线](https://help.github.com/articles/github-flavored-markdown#multiple-underscores-in-words)
*   [网址自动链接](https://help.github.com/articles/github-flavored-markdown#url-autolinking)
*   [删除线](https://help.github.com/articles/github-flavored-markdown#strikethrough)
*   [代码块](https://help.github.com/articles/github-flavored-markdown#fenced-code-blocks)
*   [代码高亮](https://help.github.com/articles/github-flavored-markdown#syntax-highlighting)

<div class="note info">
  <h5>Github 风格 Markdown 并不适用于较长的文章</h5>
  <p>
    注意 Github 风格 Markdown 是为方便评论和报告bug而创造的，并不适用于一个网站或blog。
  </p>
</div>

如果你没有[Redcarpet](https://github.com/vmg/redcarpet)，你可以用以下的命令来安装。

{% highlight sh %}
gem install redcarpet
{% endhighlight %}

