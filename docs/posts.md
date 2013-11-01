---
layout: docs
title: 撰写博客
prev_section: frontmatter
next_section: drafts
permalink: /docs/posts/
contributor: sdpfoue
---

Jeklly 的一个最好的特点是“关注 blog 本身”。这是指什么呢？简单的说就是写博客的过程被 
铸造进了 Jekyll 的功能中。你只需简单的管理你电脑中的一个文件夹下的文本文件就
可以写文章并方便的在线上发布。与繁琐的配置和维护数据库和基于网站的内容管理系统（CMS）相比，
这是一个非常受欢迎的改变。

## 文章文件夹

在[目录结构](../structure/)介绍中说明过，所有的文章都在`_posts`文件夹中。
这些文件可以用[Markdown](http://daringfireball.net/projects/markdown/) 编写，
也可以用[Textile](http://textile.sitemonks.com/) 格式编写。只要文件中有
[YAML头信息](../frontmatter/)，它们就会从源格式转化成 HTML 页面，从而成为
你的静态网站的一部分。

### 创建文章的文件

发表一篇新文章，你所需要做的就是在`_posts`文件夹中创建一个新的文件。
文件名的命名非常重要。Jekyll 要求一篇文章的文件名遵循下面的格式：
{% highlight bash %}
年-月-日-标题.MARKUP
{% endhighlight %} 
在这里，`年`是4位数字，`月`和`日`都是2位数字。`MARKUP`扩展名代表了这篇文章
是用什么格式写的。下面是一些合法的文件名的例子：
{% highlight bash %}
2011-12-31-new-years-eve-is-awesome.md
2012-09-12-how-to-write-a-blog.textile
{% endhighlight %}


### 内容格式

所有博客文章顶部必须有一段[YAML头信息](../frontmatter/)(YAML front- matter)。
在它下面，就可以选择你喜欢的格式来写文章。Jekyll支持2种流行的标记语言格式：
[Markdown](http://daringfireball.net/projects/markdown/) 和
[Textile](http://textile.sitemonks.com/). 这些格式都有自己的方式来标记文章中不
同类型的内容，所以你首先需要熟悉这些格式并选择一种最符合你需求的。

## 引用图片和其它资源

很多时候，你需要在文章中引用图片、下载或其它数字资源。尽管 Markdown 和 Textile
在链接这些资源时的语法并不一样，但你只需要关心在站点的哪些地方保存这些文件。

由于 Jekyll 的灵活性，有很多方式可以解决这个问题。一种常用做法是在工程的根目录下
创建一个文件夹，命名为`assets` 或者 `downloads`，将图片文件，下载文件或者其它的
资源放到这个文件夹下。然后在任何一篇文章中，它们都可以用站点的根目录来进行引用。
这和你站点的域名/二级域名和目录的设置相关，下面有一些例子（Markdown格式）
来演示怎样利用`site.url`变量来解决这个问题。

在文章中引用一个图片

{% highlight text %}
… 从下面的截图可以看到：
![有帮助的截图]({% raw %}{{ site.url }}{% endraw %}/assets/screenshot.jpg)
{% endhighlight %}

链接一个读者可下载的 PDF 文件：

{% highlight text %}
… 你可以直接 [下载 PDF]({% raw %}{{ site.url }}{% endraw %}/assets/mydoc.pdf).
{% endhighlight %}

<div class="note">
  <h5>提示™: 链接只使用站点的根URL</h5>
  <p>
    如果你<strong>确信</strong>你的站点只在域名的根 URL 下做展示，你可以不使用
     <code>{% raw %}{{ site.url }}{% endraw %}</code>变量。在这种情况下，
     直接使用<code>/path/file.jpg</code>即可。
  </p>
</div>

## 文章的目录

所有文章都在一个目录中是没有问题的，但是如果你不将文章列表列出来博客文章是不会被人看到
。在另一个页面上创建文章的列表（或者使用[模版](../templates/)）是很简单的。
感谢[Liquid模版语言](http://wiki.shopify.com/Liquid)和它的标记，下面
是如何创建文章列表的简单例子：

{% highlight html %}
<ul>
  {% raw %}{% for post in site.posts %}{% endraw %}
    <li>
      <a href="{% raw %}{{ post.url }}{% endraw %}">{% raw %}{{ post.title }}{% endraw %}</a>
    </li>
  {% raw %}{% endfor %}{% endraw %}
</ul>
{% endhighlight %}

当然，你可以完全控制怎样（在哪里）显示你的文章，如何管理你的站点。如果你想了解
更多你需要读一下[Jekyll 的模版是怎样工作的](../templates/)这篇文章。

## 文章摘要

Jekyll 会自动取每篇文章从开头到第一次出现`excerpt_separator`的地方作为文章的摘要，
并将此内容保存到变量`post.excerpt`中。拿上面生成文章列表的例子，你可能想在每个标题下给出文章内容的提示，你可以在每篇文章
的第一段加上如下的代码：

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

如果你不喜欢自动生成摘要，你可以在文章的YAML中增加`excerpt`来覆盖它。完全禁止掉可以
将`excerpt_separator`设置成`""`.

## 高亮代码片段

Jekyll 自带语法高亮功能，它是由 Pygments 来实现的。在文章中插入一段高亮代码非常
容易，只需使用下面的 Liquid 标记：

{% highlight text %}
{% raw %}{% highlight ruby %}{% endraw %}
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% raw %}{% endhighlight %}{% endraw %}
{% endhighlight %}

将输出下面的效果：

{% highlight ruby %}
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% endhighlight %}

<div class="note">
  <h5>提示™：显示行数</h5>
  <p>
    你可以在代码片段中增加关键字<code>linenos</code>来显示行数。
    这样完整的高亮开始标记将会是:<code>{% raw %}{% highlight ruby linenos %}{% endraw %}</code>。
  </p>
</div>

有了这些基础知识就可以开始你的第一篇文章了。当你准备更深入的了解还可以做什么的
时候，你可能会对如何[定制文章的永久链接](../permalinks/) 或在文章和站点的其它位
置中使用[定制变量](../variables/)感兴趣。
