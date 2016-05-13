---
layout: docs
title: 目录结构
permalink: /docs/structure/
translators: [Neo-J, chaucerling, TimoTokki ]
update_date: 2016-04-20
hash: 5647b91
---

Jekyll 的核心其实是一个文本转换引擎。它的概念其实就是：你用你最喜欢的标记语言来写文章，可以是 Markdown, 也可以是 Textile, 或者就是简单的 HTML, 然后 Jekyll 就会帮你套入一个或一系列的布局中。在整个过程中你可以设置 URL 路径，你的文本在布局中的显示样式等等。这些都可以通过纯文本编辑来实现，最终生成的静态页面就是你的成品了。

一个基本的 Jekyll 网站的目录结构一般是像这样的：
{% highlight bash %}
.
├── _config.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.textile
|   └── on-simplicity-in-technology.markdown
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.textile
|   └── 2009-04-26-barcamp-boston-4-roundup.textile
├── _site
├── .jekyll-metadata
└── index.html
{% endhighlight %}

来看看这些都有什么用：

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>文件 / 目录</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>_config.yml</code></p>
      </td>
      <td>
        <p>

          保存<a href="../configuration/">配置</a>数据。很多配置选项都可以直接在命令行中进行设置，但是如果你把那些配置写在这儿，你就不用非要去记住那些命令了。

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>_drafts</code></p>
      </td>
      <td>
        <p>

          drafts（草稿）是未发布的文章。这些文件的格式中都没有 <code>title.MARKUP</code> 数据。学习如何 <a href="../drafts/">使用草稿</a>.

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>_includes</code></p>
      </td>
      <td>
        <p>

          你可以加载这些包含部分到你的布局或者文章中以方便重用。可以用这个标签
          <code>{% raw %}{% include file.ext %}{% endraw %}</code>
          来把文件 <code>_includes/file.ext</code> 包含进来。

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>_layouts</code></p>
      </td>
      <td>
        <p>

          layouts（布局）是包裹在文章外部的模板。布局可以在 <a href="../frontmatter/">YAML 头信息</a>中根据不同文章进行选择。
          这将在下一个部分进行介绍。标签
          <code>{% raw %}{{ content }}{% endraw %}</code>
          可以将content插入页面中。

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>_posts</code></p>
      </td>
      <td>
        <p>

          这里放的就是你的文章了。文件格式很重要，必须要符合:
          <code>YEAR-MONTH-DAY-title.MARKUP</code>。
          <a href="../permalinks/">永久链接</a> 可以在文章中自己定制，但是数据和标记语言都是根据文件名来确定的。

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>_data</code></p>
      </td>
      <td>
        <p>

          格式化好的网站数据应放在这里。jekyll 的引擎会自动加载在该目录下所有的 yaml 文件（后缀是 <code>.yml</code>, <code>.yaml</code>, <code>.json</code> 或者 <code>.csv</code> ）。这些文件可以经由 ｀site.data｀ 访问。如果有一个 <code>members.yml</code> 文件在该目录下，你就可以通过 <code>site.data.members</code> 获取该文件的内容。

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>_site</code></p>
      </td>
      <td>
        <p>

          一旦 Jekyll 完成转换，就会将生成的页面放在这里（默认）。最好将这个目录放进你的 <code>.gitignore</code> 文件中。

        </p>
      </td>
    </tr>
     <tr>
      <td>
        <p><code>.jekyll-metadata</code></p>
      </td>
      <td>
        <p>

          该文件帮助 Jekyll 跟踪哪些文件从上次建立站点开始到现在没有被修改，哪些文件需要在下一次站点建立时重新生成。该文件不会被包含在生成的站点中。将它加入到你的 <code>.gitignore</code> 文件可能是一个好注意。

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>index.html</code> and other HTML, Markdown, Textile files</p>
      </td>
      <td>
        <p>

          如果这些文件中包含 <a href="../frontmatter/">YAML 头信息</a> 部分，Jekyll 就会自动将它们进行转换。当然，其他的如 <code>.html</code>, <code>.markdown</code>, <code>.md</code>, 或者 <code>.textile</code> 等在你的站点根目录下或者不是以上提到的目录中的文件也会被转换。

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>Other Files/Folders</p>
      </td>
      <td>
        <p>

          其他一些未被提及的目录和文件如
          <code>css</code> 还有 <code>images</code> 文件夹，
          <code>favicon.ico</code> 等文件都将被完全拷贝到生成的 site 中。这里有一些<a href="../sites/">使用 Jekyll 的站点</a>，如果你感兴趣就来看看吧。

        </p>
      </td>
    </tr>
  </tbody>
</table>
</div>
