---
layout: docs
title: 常用变量
permalink: /docs/variables/
translators: [yujingz, LeuisKen, archersmind, TimoTokki]
update_date: 2016-04-26
---

Jekyll 会遍历你的网站搜寻要处理的文件。任何有 [YAML 头信息](../frontmatter)的文件都是要处理的对象。对于每一个这样的文件，Jekyll 都会通过 [Liquid 模板工具](https://github.com/Shopify/liquid/wiki)来生成一系列的数据。下面就是这些可用数据变量的参考和文档。

## 全局(Global)变量

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>变量</th>
      <th>说明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p><code>site</code></p></td>
      <td><p>

          来自<code>_config.yml</code>文件，全站范围的信息+配置。详细的信息请参考下文

      </p></td>
    </tr>
    <tr>
      <td><p><code>page</code></p></td>
      <td><p>

        页面专属的信息 + <a href="../frontmatter/">YAML 头文件信息</a>。通过 YAML 头文件自定义的信息都可以在这里被获取。详情请参考下文。

      </p></td>
    </tr>
    <tr>
      <td><p><code>layout</code></p></td>
      <td><p>

        Layout specific information + the <a href="../frontmatter/">YAML front
        matter</a>. Custom variables set via the YAML Front Matter in
        layouts will be available here.

      </p></td>
    </tr>
    <tr>
      <td><p><code>content</code></p></td>
      <td><p>

        被 layout 包裹的那些 Post 或者 Page 渲染生成的内容。但是又没定义在 Post 或者 Page 文件中的变量。

      </p></td>
    </tr>
    <tr>
      <td><p><code>paginator</code></p></td>
      <td><p>

        每当 <code>paginate</code> 配置选项被设置了的时候，这个变量就可用了。详情请看<a
        href="../pagination/">分页</a>。

      </p></td>
    </tr>
  </tbody>
</table>
</div>

## 全站(site)变量

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>变量</th>
      <th>说明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p><code>site.time</code></p></td>
      <td>
        <p>

        当前时间（运行<code>jekyll</code>这个命令的时间点）。

        </p>
        <p>
        
        如果你发布在
        <code>GitHub Pages</code>
        或其它类似主机上，你每一次的
        <code>commit</code>
        都会触发这个操作。
        
        </p>
      </td>
    </tr>
    <tr>
      <td><p><code>site.pages</code></p></td>
      <td><p>

        所有 Pages 的清单。

      </p></td>
    </tr>
    <tr>
      <td><p><code>site.posts</code></p></td>
      <td><p>

        一个按照时间倒序的所有 Posts 的清单。

      </p></td>
    </tr>
    <tr>
      <td><p><code>site.related_posts</code></p></td>
      <td><p>

        如果当前被处理的页面是一个 Post，这个变量就会包含最多10个相关的 Post。默认的情况下，相关性是低质量的，但是能被很快的计算出来。如果你需要高相关性，就要消耗更多的时间来计算。用 <code>jekyll</code> 这个命令带上 <code>--lsi</code> (latent semantic
        indexing) 选项来计算高相关性的 Post。注意，GitHub 在生成站点时不支持　<code>lsi</code>。

      </p></td>
    </tr>
    <tr>
      <td><p><code>site.static_files</code></p></td>
      <td><p>

        <a href="/docs/static-files/">静态文件</a>的列表 (此外的文件不会被 Jekyll 和 Liquid 处理。)。每个文件都具有三个属性： <code>path</code>，  <code>modified_time</code> 以及 <code>extname</code>。

      </p></td>
    </tr>
    <tr>
      <td><p><code>site.html_pages</code></p></td>
      <td><p>

        ‘site.pages’的子集，存储以‘.html’结尾的部分。

      </p></td>
    </tr>
    <tr>
      <td><p><code>site.html_files</code></p></td>
      <td><p>

        ‘site.static_files’的子集，存储以‘.html’结尾的部分。

      </p></td>
    </tr>
    <tr>
      <td><p><code>site.collections</code></p></td>
      <td><p>

        一个所有集合（collection）的清单。

      </p></td>
    </tr>
    <tr>
      <td><p><code>site.data</code></p></td>
      <td><p>

        一个存储了 <code>_data</code> 目录下的YAML文件数据的清单。

      </p></td>
    </tr>
    <tr>
      <td><p><code>site.documents</code></p></td>
      <td><p>

        每一个集合（collection）中的全部文件的清单。

      </p></td>
    </tr>
    <tr>
      <td><p><code>site.categories.CATEGORY</code></p></td>
      <td><p>

        所有的在 <code>CATEGORY</code> 类别下的帖子。

      </p></td>
    </tr>
    <tr>
      <td><p><code>site.tags.TAG</code></p></td>
      <td><p>

        所有的在 <code>TAG</code> 标签下的帖子。

      </p></td>
    </tr>
    <tr>
      <td><p><code>site.[CONFIGURATION_DATA]</code></p></td>
      <td><p>
        所有的通过命令行和 <code>_config.yml</code> 设置的变量都会存到这个 <code>site</code> 里面。
        举例来说，如果你设置了 <code>url: http://mysite.com</code> 在你的配置文件中，那么在你的 Posts
        和 Pages 里面，这个变量就被存储在了 <code>site.url</code>。Jekyll 并不会把对 <code>_config.yml</code>
        做的改动放到 <code>watch</code> 模式，所以你每次都要重启 Jekyll 来让你的变动生效。
      </p></td>
    </tr>
  </tbody>
</table>
</div>

## 页面(page)变量

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>变量</th>
      <th>说明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p><code>page.content</code></p></td>
      <td><p>

        页面内容的源码。

      </p></td>
    </tr>
    <tr>
      <td><p><code>page.title</code></p></td>
      <td><p>

        页面的标题。

      </p></td>
    </tr>
    <tr>
      <td><p><code>page.excerpt</code></p></td>
      <td><p>

        页面摘要的源码。

      </p></td>
    </tr>
    <tr>
      <td><p><code>page.url</code></p></td>
      <td><p>

        帖子以斜线打头的相对路径，例子： <code>/2008/12/14/my-post.html</code>。

      </p></td>
    </tr>
    <tr>
      <td><p><code>page.date</code></p></td>
      <td><p>

        帖子的日期。日期的可以在帖子的头信息中通过用以下格式
        <code>YYYY-MM-DD HH:MM:SS</code> (假设是 UTC), 或者
        <code>YYYY-MM-DD HH:MM:SS +/-TTTT</code> ( 用于声明不同于 UTC 的时区，
        比如 <code>2008-12-14 10:30:00 +0900</code>) 来显示声明其他 日期/时间 的方式被改写，

      </p></td>
    </tr>
    <tr>
      <td><p><code>page.id</code></p></td>
      <td><p>

        帖子的唯一标识码（在RSS源里非常有用），比如
        <code>/2008/12/14/my-post</code>

      </p></td>
    </tr>
    <tr>
      <td><p><code>page.categories</code></p></td>
      <td><p>

        这个帖子所属的 Categories。Categories 是从这个帖子的 <code>_posts</code> 以上
        的目录结构中提取的。举例来说, 一个在 <code>/work/code/_posts/2008-12-24-closures.md</code>
        目录下的 Post，这个属性就会被设置成 <code>['work', 'code']</code>。不过 Categories 也能在
        <a href="../frontmatter/">YAML 头文件信息</a> 中被设置。

      </p></td>
    </tr>
    <tr>
      <td><p><code>page.tags</code></p></td>
      <td><p>

        这个 Post 所属的所有 tags。Tags 是在<a href="../frontmatter/">YAML 头文件信息</a>中被定义的。

      </p></td>
    </tr>
    <tr>
      <td><p><code>page.path</code></p></td>
      <td><p>

        Post 或者 Page 的源文件地址。举例来说，一个页面在 GitHub 上的源文件地址。
        这可以在 <a href="../frontmatter/">YAML 头文件信息</a> 中被改写。

      </p></td>
    </tr>
    <tr>
      <td><p><code>page.next</code></p></td>
      <td><p>

        当前文章在<code>site.posts</code>中的位置对应的下一篇文章。若当前文章为最后一篇文章，返回<code>nil</code>

      </p></td>
    </tr>
    <tr>
      <td><p><code>page.previous</code></p></td>
      <td><p>

      当前文章在<code>site.posts</code>中的位置对应的上一篇文章。若当前文章为第一篇文章，返回<code>nil</code>

      </p></td>
    </tr>
  </tbody>
</table>
</div>

<div class="note">
  <h5>提示™: 使用自定义的头信息</h5>
  <p>

    任何你自定义的头文件信息都会在 <code>page</code> 中可用。
    举例来说，如果你在一个 Page 的头文件中设置了 <code>custom_css: true</code>，
    这个变量就可以这样被取到 <code>page.custom_css</code>。

  </p>
  <p>

    If you specify front matter in a layout, access that via <code>layout</code>.
    For example, if you specify <code>class: full_page</code>
    in a page’s front matter, that value will be available as
    <code>layout.class</code> in the layout and its parents.

  </p>
</div>

## 分页器(Paginator)

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>变量</th>
      <th>说明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p><code>paginator.per_page</code></p></td>
      <td><p>每一页 Posts 的数量。</p></td>
    </tr>
    <tr>
      <td><p><code>paginator.posts</code></p></td>
      <td><p>这一页可用的 Posts。</p></td>
    </tr>
    <tr>
      <td><p><code>paginator.total_posts</code></p></td>
      <td><p>Posts 的总数。</p></td>
    </tr>
    <tr>
      <td><p><code>paginator.total_pages</code></p></td>
      <td><p>Pages 的总数。</p></td>
    </tr>
    <tr>
      <td><p><code>paginator.page</code></p></td>
      <td><p>当前页号。</p></td>
    </tr>
    <tr>
      <td><p><code>paginator.previous_page</code></p></td>
      <td><p>前一页的页号。</p></td>
    </tr>
    <tr>
      <td><p><code>paginator.previous_page_path</code></p></td>
      <td><p>前一页的地址。</p></td>
    </tr>
    <tr>
      <td><p><code>paginator.next_page</code></p></td>
      <td><p>下一页的页号。</p></td>
    </tr>
    <tr>
      <td><p><code>paginator.next_page_path</code></p></td>
      <td><p>下一页的地址。</p></td>
    </tr>
  </tbody>
</table>
</div>

<div class="note info">
  <h5>分页器变量的可用性</h5>
  <p>
    这些变量仅在首页文件中可用，不过他们也会存在于子目录中，就像 <code>/blog/index.html</code>。
  </p>
</div>
