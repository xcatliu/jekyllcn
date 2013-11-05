---
layout: docs
title: 头信息 
prev_section: configuration
next_section: posts
permalink: /docs/frontmatter/
contributor: liul85
---

正是头信息开始让 Jekyll 变的很酷。任何只要包含 [YAML](http://yaml.org/) 头信息的文件在 Jekyll 中都能被当做一个特殊的文件来处理。头信息必须在文件的开始部分，并且需要按照 YAML 的格式写在两行三虚线之间。下面是一个基本的例子：

{% highlight yaml %}
---
layout: post
title: Blogging Like a Hacker
---
{% endhighlight %}

在这两行的三虚线之间，你可以设置一些预定义的变量（下面这个例子可以作为参考）或者甚至创建一个你自己定义的变量。这样在接下来的文件和任意模板中或者在包含这些页面或博客的模板中都可以通过使用 Liquid 标签来访问这些变量。

<div class="note warning">
  <h5>UTF-8 编码方式警告</h5>
  <p>
    如果你使用UTF-8编码，那么在你的文件中一定不要出现 <code>BOM</code> 头字符，否则你会碰上非常糟糕的事情，尤其当你在Windows上使用Jekyll的时候。
  </p>
</div>

<div class="note">
  <h5>提示™：头信息变量是可选的</h5>
  <p>
    如果你想使用 <a href="../variables/">Liquid 标签和变量</a>但是在头信息中又不需要任何定义，那么你可以将头信息设置为空！在头信息为空的情况下，Jekyll 仍然能够处理文件。（这对于一些像 CSS 和 RSS 的文件非常有用）
  </p>
</div>

## 预定义的全局变量 

你可以在页面或者博客的头信息处使用一些已经预定义好的全局变量。

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>变量名称</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>layout</code></p>
      </td>
      <td>
        <p>

          如果设置的话，会指定使用该模板文件。指定模板文件时候不需要扩展名。模板文件需要放在 <code>_layouts</code> 目录下。

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>permalink</code></p>
      </td>
      <td>
        <p>

          如果你需要让你的博客中的URL地址不同于默认值 <code>/year/month/day/title.html</code> 这样，那么当你设置这个变量后，就会使用最终的URL地址。

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>published</code></p>
      </td>
      <td>
        <p>
          当站点生成的时候，如果你不需要展示一个具体的博文，可以设置这个变量为 false。

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p style="margin-bottom: 5px;"><code>category</code></p>
        <p><code>categories</code></p>
      </td>
      <td>
        <p>

          除过将博客文章放在某个文件夹下面外，你还可以根据文章的类别来给他们设置一个或者多个分类属性。这样当你的博客生成的时候这些文章就可以根据这些分类来阅读。在一个文章中多个类别可以通过 <a href="http://en.wikipedia.org/wiki/YAML#Lists">YAML list</a>来指定，或者用空格隔开。

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>tags</code></p>
      </td>
      <td>
        <p>

          类似分类，一篇文章也可以给它增加一个或者多个标签。同样多个标签之间可以通过 YAML 列表或者空格隔开。

        </p>
      </td>
    </tr>
  </tbody>
</table>
</div>


## 自定义变量

在头信息中没有预先定义的任何变量都会在数据转换中通过 Liquid 模板被调用。例如，在头信息中你设置一个 title，然后就可以在你的模板中使用这个 title 变量来设置页面的 title属性 ：

{% highlight html %}
<!DOCTYPE HTML>
<html>
  <head>
    <title>{% raw %}{{ page.title }}{% endraw %}</title>
  </head>
  <body>
    ...
{% endhighlight %}

## 在文章中预定义的变量

在文章中可以使用这些在头信息变量列表中未包含的变量。

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>变量名称</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>date</code></p>
      </td>
      <td>
        <p>
          这里的日期会覆盖文章名字中的日期。这样就可以用来确定文章分类的正确。
        </p>
      </td>
    </tr>
  </tbody>
</table>
</div>
