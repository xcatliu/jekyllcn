---
layout: docs
title: 分页功能
prev_section: permalinks
next_section: plugins
permalink: /docs/pagination/
contributor: debbbbie
---

对于大多数网站（尤其是博客），当文章越来越多的时候，就会有分页显示文章列表的需求。 Jekyll已经自建
分页功能，你只需要根据约定放置文件即可。

<div class="note info">
  <h5>分页功能只支持 HTML 文件</h5>
  <p>
    Jekyll 的分页功能不支持 Markdown 或 Textile 文件，而是只支持 HTML 文件。当然，这不会让
    你不爽。
  </p>
</div>

## 开启分页功能

开启分页功能很简单，只需要在 `_config.yml`里边加一行，并填写每页需要几行：

{% highlight yaml %}
paginate: 5
{% endhighlight %}

下边是对需要带有分页页面的配置：

{% highlight yaml %}
paginate_path: "blog/page:num"
{% endhighlight %}

`blog/index.html`将会读取这个设置，把他传给每个分页页面，然后从第 `2` 页开始输出到
 `blog/page:num` ， `:num` 是页码。如果有 12 篇文章并且做如下配置 `paginate: 5` ，
 Jekyll会将前 5 篇文章写入 `blog/index.html` ，把接下来的 5 篇文章写入
 `blog/page2/index.html`，最后 2 篇写入 `blog/page3/index.html`。

## 与 `paginator` 相同的属性

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
              上一页页码 或 <code>nil</code>
          </p>
      </td>
    </tr>
    <tr>
      <td><p><code>previous_page_path</code></p></td>
      <td>
          <p>
              上一页路径 或 <code>nil</code>
          </p>
      </td>
    </tr>
    <tr>
      <td><p><code>next_page</code></p></td>
      <td>
          <p>
              下一页页码 或 <code>nil</code>
          </p>
      </td>
    </tr>
    <tr>
      <td><p><code>next_page_path</code></p></td>
      <td>
          <p>
              下一页路径 或 <code>nil</code>
          </p>
      </td>
    </tr>
  </tbody>
</table>
</div>

<div class="note info">
  <h5>不支持对“标签”和“类别”分页</h5>
  <p>分页功能仅仅遍历文章列表并计算出结果，并无读取 YAML 头信息，现在不支持对“标签”和“类别”分页。</p>
</div>

## 生成带分页功能的文章

接下来要做的事情就是展现在页面上了，下边是一个简单的例子：

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
    Jekyll 没有生成文件夹 ‘page1’ ，所以上边的代码有 bug ，下边的代码解决了这个问题。
  </p>
</div>

 下边的 HTML 片段是第一页，他除自己外，为每个页面生成了链接。

{% highlight html %}
{% raw %}
<div id="post-pagination" class="pagination">
  {% if paginator.previous_page %}
    <p class="previous">
      {% if paginator.previous_page == 1 %}
        <a href="/">Previous</a>
      {% else %}
        <a href="{{ paginator.previous_page_path }}">Previous</a>
      {% endif %}
    </p>
  {% else %}
    <p class="previous disabled">
      <span>Previous</span>
    </p>
  {% endif %}

  <ul class="pages">
    <li class="page">
      {% if paginator.page == 1 %}
        <span class="current-page">1</span>
      {% else %}
        <a href="/">1</a>
      {% endif %}
    </li>

    {% for count in (2..paginator.total_pages) %}
      <li class="page">
        {% if count == paginator.page %}
          <span class="current-page">{{ count }}</span>
        {% else %}
          <a href="/page{{ count }}">{{ count }}</a>
        {% endif %}
      </li>
    {% endfor %}
  </ul>

  {% if paginator.next_page %}
    <p class="next">
      <a href="{{ paginator.next_page_path }}">Next</a>
    </p>
  {% else %}
    <p class="next disabled">
      <span>Next</span>
    </p>
  {% endif %}

</div>
{% endraw %}
{% endhighlight %}
