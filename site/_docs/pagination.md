---
layout: docs
title: 分页功能
permalink: /docs/pagination/
translators: [debbbbie, TimoTokki]
update_date: 2016-05-04
---

对于大多数网站（尤其是博客），当文章越来越多的时候，就会有分页显示文章列表的需求。Jekyll 已经自建分页功能，你只需要根据约定放置文件即可。

在 Jekyll 3 中，需要在 gems 中安装 `jekyll-paginate` 插件，并添加到你的 Gemfile 和 `_config.yml` 中。在 Jekyll 2 中，分页是标准功能。

<div class="note info">
  <h5>分页功能只支持 HTML 文件</h5>
  <p>
    Jekyll 的分页功能不支持 Jekyll site 中的 Markdown 或 Textile 文件。分页功能从名为 <code>index.html</code> 的 HTML 文件中被调用时，才能工作。分页功能是可选的，可能通过 <code>paginate_path</code> 配置的值，驻留和生成在子目录中。
  </p>
</div>

## 开启分页功能

开启分页功能很简单，只需要在 `_config.yml` 里边加一行，指明每页该展示多少项目：

{% highlight yaml %}
paginate: 5
{% endhighlight %}

这个数字应当是你希望在生成的站点中每页展示博客数目的最大值。

你可能还需要指定分页页面的目标路径：

{% highlight yaml %}
paginate_path: "blog/page:num"
{% endhighlight %}

`blog/index.html` 将会读取这个设置，把它传给每个分页页面，然后从第 `2` 页开始输出到 `blog/page:num`, `:num` 是页码。如果有 12 篇文章并且做如下配置 `paginate: 5`, Jekyll 会将前 5 篇文章写入 `blog/index.html`，把接下来的 5 篇文章写入 `blog/page2/index.html`，最后 2 篇写入 `blog/page3/index.html`。

<div class="note warning">
  <h5>不要设置 permalink</h5>
  <p>
    在你的博客的头信息中设置 permalink 会造成分页功能的瘫痪。缺省设置 permalink 即可。
  </p>
</div>

## 可用的 Liquid 属性

分页功能插件使得 `paginator` liquid 对象具有下列属性：

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>属性</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p><code>page</code></p></td>
      <td><p>当前页码</p></td>
    </tr>
    <tr>
      <td><p><code>per_page</code></p></td>
      <td><p>每页文章数量</p></td>
    </tr>
    <tr>
      <td><p><code>posts</code></p></td>
      <td><p>当前页的文章列表</p></td>
    </tr>
    <tr>
      <td><p><code>total_posts</code></p></td>
      <td><p>总文章数</p></td>
    </tr>
    <tr>
      <td><p><code>total_pages</code></p></td>
      <td><p>总页数</p></td>
    </tr>
    <tr>
      <td><p><code>previous_page</code></p></td>
      <td>
          <p>
              上一页页码 或 <code>nil</code>（如果上一页不存在）
          </p>
      </td>
    </tr>
    <tr>
      <td><p><code>previous_page_path</code></p></td>
      <td>
          <p>
              上一页路径 或 <code>nil</code>（如果上一页不存在）
          </p>
      </td>
    </tr>
    <tr>
      <td><p><code>next_page</code></p></td>
      <td>
          <p>
              下一页页码 或 <code>nil</code>（如果下一页不存在）
          </p>
      </td>
    </tr>
    <tr>
      <td><p><code>next_page_path</code></p></td>
      <td>
          <p>
              下一页路径 或 <code>nil</code>（如果下一页不存在）
          </p>
      </td>
    </tr>
  </tbody>
</table>
</div>

<div class="note info">
  <h5>不支持对“标签”和“类别”分页</h5>
  <p>分页功能遍历 <code>posts</code> 下的所有文章，而忽略定义在文章内的头信息中的变量。现在不支持对“标签”和“类别”分页。也不支持任何文件集合，因为该功能被限制在 posts 中。</p>
</div>

## 生成带分页功能的文章

接下来你需要做的事情，就是使用你已经掌握的 `paginator` 变量，列表展示你的文章。下边是一个简单的例子，在 HTML 文件中生成带分页功能的文章：

{% highlight html %}
{% raw %}
---
layout: default
title: My Blog
---

<!-- 遍历分页后的文章 -->
{% for post in paginator.posts %}
  <h1><a href="{{ post.url }}">{{ post.title }}</a></h1>
  <p class="author">
    <span class="date">{{ post.date }}</span>
  </p>
  <div class="content">
    {{ post.content }}
  </div>
{% endfor %}

<!-- 分页链接 -->
<div class="pagination">
  {% if paginator.previous_page %}
    <a href="/page{{ paginator.previous_page }}" class="previous">Previous</a>
  {% else %}
    <span class="previous">Previous</span>
  {% endif %}
  <span class="page_number ">Page: {{ paginator.page }} of {{ paginator.total_pages }}</span>
  {% if paginator.next_page %}
    <a href="/page{{ paginator.next_page }}" class="next">Next</a>
  {% else %}
    <span class="next ">Next</span>
  {% endif %}
</div>
{% endraw %}
{% endhighlight %}

<div class="note warning">
  <h5>注意首尾页</h5>
  <p>
    Jekyll 不会生成文件夹 ‘page1’，所以如上代码在遇到 <code>/page1</code> 这样的链接时会出错。如果你遇到该问题，可以查看下边的解决方案。
  </p>
</div>

 下边的 HTML 片段能够处理第一页，为除当前页面外的每个页面生成链接。

{% highlight html %}
{% raw %}
{% if paginator.total_pages > 1 %}
<div class="pagination">
  {% if paginator.previous_page %}
    <a href="{{ paginator.previous_page_path | prepend: site.baseurl | replace: '//', '/' }}">&laquo; Prev</a>
  {% else %}
    <span>&laquo; Prev</span>
  {% endif %}

  {% for page in (1..paginator.total_pages) %}
    {% if page == paginator.page %}
      <em>{{ page }}</em>
    {% elsif page == 1 %}
      <a href="{{ paginator.previous_page_path | prepend: site.baseurl | replace: '//', '/' }}">{{ page }}</a>
    {% else %}
      <a href="{{ site.paginate_path | prepend: site.baseurl | replace: '//', '/' | replace: ':num', page }}">{{ page }}</a>
    {% endif %}
  {% endfor %}

  {% if paginator.next_page %}
    <a href="{{ paginator.next_page_path | prepend: site.baseurl | replace: '//', '/' }}">Next &raquo;</a>
  {% else %}
    <span>Next &raquo;</span>
  {% endif %}
</div>
{% endif %}
{% endraw %}
{% endhighlight %}
