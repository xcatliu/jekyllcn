---
layout: docs
title: 撰写博客
permalink: /docs/posts/
translators: [sdpfoue, LeuisKen, archersmind, TimoTokki]
update_date: 2016-04-22
---

JJekyll的一个长处就是便于博客写作。这句话从何说起呢？简单的说，Jekyll从功能上天然地适合写博客，
因为要完成写文章并po到网上去这种事，你只需要在自己电脑上管理一个文件夹和一系列文本文件就好了，
它就是一个再简单不过的Blog。比起搭建和维护一个数据库，再加一个WEB内容管理系统的种种繁琐来说，这显然是一个喜闻乐见的进步！

## 文章文件夹

在Jekyll中，名为 `_posts` 的文件夹是你放博文的地方。这里面的文章通常使用 [Markdown](http://daringfireball.net/projects/markdown/) 编写，或 HTML语法写成，也可以是其他格式，只要你安装了配套的格式转换器就行。所有的博文都必须有 [YAML Front Matter](../frontmatter/)头信息，并且它们最终在你的静态网站中会被转换为HTML格式的页面。

### 创建博文

通过在`_posts`文件夹中创建一个新文件来创作并发表一篇新博文。重点要注意的是文件名，它应该符合如下格式：

```sh
YEAR-MONTH-DAY-title.MARKUP
```
其中 `YEAR` 是4个数字的年份， `MONTH` 和 `DAY` 是2位数的月份和日。最后的文件扩展名 `MARKUP` 代表文件的格式。下面是几个例子:

```sh
2011-12-31-new-years-eve-is-awesome.md
2012-09-12-how-to-write-a-blog.md
```

<div class="note">
  <h5>提示™: 链接到其他博文</h5>
  <p>
    使用 <code><a href="../templates/#post-url">post_url</a></code> 标签链接到你的其他博文，以免网站的 permalink 变量改变产生不必要的麻烦。
  </p>
</div>

### 内容格式

所有博客文章顶部必须有一段 [YAML 头信息](../frontmatter/)(YAML front- matter)。在它下面，就可以选择你喜欢的格式来写文章。 Jekyll 支持 [Markdown](http://daringfireball.net/projects/markdown/)，以及[其他众多格式的扩展](/docs/plugins/#converters-1)，其中就包括十分流行的 [Textile](http://redcloth.org/textile)。这些格式都有自己的方式来标记文章中不同类型的内容，所以你首先需要熟悉这些格式并选择一种最符合你需求的。

<div class="note info">
  <h5>注意字符集</h5>
  <p>
    为了让内容中的一些字符看上去更美观，内容处理程序会修改它们。例如，<code>smart</code>扩展会根据Redcarpet转换标准将ASCII的引号字符（”）为Unicode中的花括号（{）。为了让浏览器正确显示这些字符，请在<code>&lt;head&gt;</code>中包含进字符集的元值，即<code>&lt;meta charset=&quot;utf-8&quot;&gt;</code>。
  </p>
</div>

## 引用图片和其它资源

你显然会有需求在博文中插入图片、附件以及其他各种资源。除了要考虑在Markdown或Textile两种语法中，怎么做链接的语法以外，将图片等资源放在哪里也是要考虑的一个问题。

由于 Jekyll 的灵活性，有很多方式可以解决这个问题。一种常用做法是在工程的根目录下创建一个文件夹，命名为　`assets` 或者 `downloads`，将图片文件，下载文件或者其它的资源放到这个文件夹下。然后在你的博文中就可以使用assets文件夹在网站根目录下的路径作为网址链接这些附件了。但需要强调一个前提，就是你博客的配置文件中把域名和访问路径已经配置好了。 以下是在博文中通过Markdown语法做链接的几个例子，注意 `site.url`的使用。

在博文中插入一个图片：

```text
... 截图如下:
![屏幕截图1]({% raw %}{{ site.url }}{% endraw %}/assets/screenshot.jpg)
```

放一个PDF链接让你的读者下载:

```text
... 请 [下载PDF]({% raw %}{{ site.url }}{% endraw %}/assets/mydoc.pdf)。
```

<div class="note">
  <h5>提示™：链接只使用站点的根 URL</h5>
  <p>
    若能确保你的博客永远都可以通过域名下的根目录访问，那你也可以在链接时省略 <code>{% raw %}{{ site.url }}{% endraw %}</code>变量。要是这样的话，对图片附件等做链接时，你也可以直接这样写<code>/path/file.jpg</code>。
  </p>
</div>

## 一个典型的博文

Jekyll 能处理很多不同的你能想象到的跟博文有关的特性，但是总的来说一个典型的博文一般包含标题、排版、发布日期，和栏目，它的文本格式看起来像下面这样:

```
---
layout: post
title:  "世界，你好!"
date:   2015-11-17 16:16:01 -0600
categories: 测试栏目
---
博文正文开始了，一下英文请别看，都是例子。

You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `bundle exec jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

```
位于第一个和第二个`---`之间的所有内容都被识别为YAML Front Matter的部分，在其后的所有内容都会被按照Markdown语法处理转换，作为博文正文展示。

## 文章的目录

光写一篇篇的博文别人看不到也没用啊，你总得弄一个入口页面把它列出来吧。好在有[Liquid template
language](https://docs.shopify.com/themes/liquid/basics) 的语法标签，我们新建一个页面（或在[模板里](../templates/)）并在里面列出博文目录索引也不难的。以下就是一个列出博文的示例:

```html
<ul>
  {% raw %}{% for post in site.posts %}{% endraw %}
    <li>
      <a href="{% raw %}{{ post.url }}{% endraw %}">{% raw %}{{ post.title }}{% endraw %}</a>
    </li>
  {% raw %}{% endfor %}{% endraw %}
</ul>
```

至于怎么显示博文，怎么组织网站结构，完全取决于你。不过动手之前你得进一步学习Jekyll中[模板是怎么工作的](../templates/)。

注意一下，上面例子中的`post`变量只存在于`for`循环之内。如果你想操作当前正在渲染的整个页面（或博文）（也就是`for`所在的这整个页面），请改用`page`变量。

## 文章摘要

Jekyll 会自动取每篇文章从开头到第一次出现 `excerpt_separator` 的地方作为文章的摘要，并将此内容保存到变量 `post.excerpt` 中。拿上面生成文章列表的例子，你可能想在每个标题下给出文章内容的提示，你可以在每篇文章的第一段加上如下的代码：

{% highlight html %}
<ul>
  {% raw %}{% for post in site.posts %}{% endraw %}
    <li>
      <a href="{% raw %}{{ post.url }}{% endraw %}">{% raw %}{{ post.title }}{% endraw %}</a>
      <p>{% raw %}{{ post.excerpt }}{% endraw %}</p>
    </li>
  {% raw %}{% endfor %}{% endraw %}
</ul>
{% endhighlight %}

由于 Jekyll 会提取第一段的内容，你没有必要将摘要包裹在 `p` 标签中，它已经为你做了这项工作。如果你希望移除它们可以使用如下的代码：

{% highlight html %}
{% raw %}{{ post.excerpt | remove: '<p>' | remove: '</p>' }}{% endraw %}
{% endhighlight %}

如果你不喜欢自动生成摘要，你可以在文章的 YAML 头信息中增加 `excerpt` 来覆盖它。另外，你也可以选择在文章中自定义一个 `excerpt_separator`:

{% highlight text %}
---
excerpt_separator: <!--more-->
---

Excerpt
<!--more-->
Out-of-excerpt
{% endhighlight %}

你也可以在 `_config.yml` 中全局声明 `excerpt_separator`。

完全禁止掉可以将 `excerpt_separator` 设置成 `""`。

同时，对于由 Liquid 标签输出的内容，你可以通过`| strip_html`过滤器来移除输出内容中的html标签。这在某些场景，如在你博文的`head`中生成`meta="description"`，以及其他html标签与内容不应混杂的场景下很有帮助。

## 高亮代码片段

Jekyll还原生支持码农喜闻乐见的代码语法高亮。高亮功能由Rouge和Pygments两个库提供支持，默认是Rouge。

使用如下的Liquid模板语法：

```text
{% raw %}{% highlight ruby %}{% endraw %}
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% raw %}{% endhighlight %}{% endraw %}
```

得到的效果如下:

```ruby
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
```

<div class="note">
  <h5>提示™：显示行数</h5>
  <p>
    你可以在代码片段中增加关键字 <code>linenos</code> 来显示行数。这样完整的高亮开始标记将会是: <code>{% raw %}{% highlight ruby linenos %}{% endraw %}</code>。
  </p>
</div>

有了这些基础知识就可以开始你的第一篇文章了。当你准备更深入的了解还可以做什么的时候，你可能会对如何[定制文章的永久链接](../permalinks/) 或在文章和站点的其它位置中使用[定制变量](../variables/)感兴趣。
