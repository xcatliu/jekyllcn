---
layout: docs
title: 永久链接
permalink: /docs/permalinks/
translators: [debbbbie, TimoTokki]
update_date: 2016-05-04
---

Jekyll 支持以灵活的方式管理你网站的链接，你可以通过 [Configuration](../configuration/) 或 [YAML 头信息](../frontmatter/) 为每篇文章设置永久链接。你可以随心所欲地选择内建链接格式，或者自定义链接格式。默认配置为 `date`。

永久链接的模板用以冒号为前缀的关键词标记动态内容，比如 `date` 代表 `/:categories/:year/:month/:day/:title.html`。

## 模板变量

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>变量</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>year</code></p>
      </td>
      <td>
        <p>文章文件名中的年份，格式如 `2013`</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>month</code></p>
      </td>
      <td>
        <p>文章文件名中的月份，格式如 `01`</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>i_month</code></p>
      </td>
      <td>
        <p>文章文件名中的月份，不包含首位的零，格式如 `1`</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>day</code></p>
      </td>
      <td>
        <p>文章文件名中的日期，格式如 `08`</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>i_day</code></p>
      </td>
      <td>
        <p>文章文件名中的日期，不包含首位的零，格式如 `8`</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>short_year</code></p>
      </td>
      <td>
        <p>文章文件名中的年份，后两位，格式如 `13`</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>hour</code></p>
      </td>
      <td>
        <p>
          时钟，24 小时制，日期以文章的头信息中的 <code>date</code> 为基准。（00..23）
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>minute</code></p>
      </td>
      <td>
        <p>
          当前时钟内的分钟，日期以文章的头信息中的 <code>date</code> 为基准。（00..59）
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>second</code></p>
      </td>
      <td>
        <p>
          当前分钟内的秒钟，日期以文章的头信息中的 <code>date</code> 为基准。（00..59）
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>title</code></p>
      </td>
      <td>
        <p>由文件的文件名中确定的标题，可以被文件头信息中的 <code>slug</code> 覆盖。</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>slug</code></p>
      </td>
      <td>
        <p>
            由文件的文件名中确定的　Slugified title（除数字和字母之外的字符们会被取代为连字符），可以被文件头信息中的 <code>slug</code> 覆盖。
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>categories</code></p>
      </td>
      <td>
        <p>
          文章类型。如果一篇文章有多个类型，Jekyll 会创建一个目录（例如，<code>/category1/category2</code>）。Jekyll 也可以自动解析 URLs 中的双斜线 `//`，所以如果当前文章没有设定类型，则忽略该项。
        </p>
      </td>
    </tr>
  </tbody>
</table>
</div>

## 内建永久链接类型

当你能够通过 [template variables](#template-variables) 来指定一个自定义永久链接时，方便起见，Jekyll 还提供了下列的内建类型。

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>永久链接类型</th>
      <th> URL 模板</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>date</code></p>
      </td>
      <td>
        <p><code>/:categories/:year/:month/:day/:title.html</code></p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>pretty</code></p>
      </td>
      <td>
        <p><code>/:categories/:year/:month/:day/:title/</code></p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>ordinal</code></p>
      </td>
      <td>
        <p><code>/:categories/:year/:y_day/:title.html</code></p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>none</code></p>
      </td>
      <td>
        <p><code>/:categories/:title.html</code></p>
      </td>
    </tr>
  </tbody>
</table>
</div>

## 页面（Pages） 和集合（collections）

`permalink` 配置用来指定博客的永久链接模板。页面和集合同样有它们自己的默认永久链接模板；页面的默认模板是 `/:path/:basename`，集合的默认模板是 /:collection/:path`。

这些样式被修改用来匹配在文章永久链接设置里的后缀式。例如，含有反斜杠 `/` 的永久链接模板 `pretty` 会更新页面的永久链接，使其同样包含一个反斜杠：
`/:path/:basename/`。含有文件扩展名的永久链接模板 `date` 会更新页面的永久链接，使其同样包含文件扩展名：
`/:path/:basename:output_ext`。这对任意自定义永久链接模板同样适用。

单独页面或集合文件的永久链接总能够在页面或者文件的[头信息](../frontmatter/)里重写覆盖。另外，给定的集合的永久链接能在[集合配置](../collections/)中自定义设置。

## 永久链接模板举例

比如文件名： `/2009-04-29-slap-chop.textile`

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>URL 模板</th>
      <th>对应的永久链接 URL </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>没有配置或 <code>permalink: date</code></p>
      </td>
      <td>
        <p><code>/2009/04/29/slap-chop.html</code></p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>pretty</code></p>
      </td>
      <td>
        <p><code>/2009/04/29/slap-chop/</code></p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>/:month-:day-:year/:title.html</code></p>
      </td>
      <td>
        <p><code>/04-29-2009/slap-chop.html</code></p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>/blog/:year/:month/:day/:title</code></p>
      </td>
      <td>
        <p><code>/blog/2009/04/29/slap-chop/index.html</code></p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>/:year/:month/:title</code></p>
        <p>具体细节见于 <a href="#extensionless-permalinks">无扩展名链接（Extensionless permalinks）</a>。</p>
      </td>
      <td>
        <p><code>/2009/04/slap-chop</code></p>
      </td>
    </tr>
  </tbody>
</table>
</div>

## 无扩展名永久链接（Extensionless permalinks）

Jekyll 支持即不包含反斜杠也不包含文件扩展名的永久链接，但这需要网络服务端的额外支持才能正常工作。当使用无扩展名永久链接时，写到硬盘上的输出文件依然会保留正确的文件扩展名（典型的比如，`.html`），所以网络服务端必须能够 map 那些没有文件扩展名的文件的请求。

无论 [GitHub Pages](../github-pages/) 还是 Jekyll 内置的 WEBrick server 都能够正确处理这些请求，不需要任何额外工作。

### Apache

Apache 网络服务端对内容协商（content negotiation）有着非常广泛的支持，而且能够通过在你的 `httpd.conf` 或者 `.htaccess` 文件中设置 [multiviews][] 选项来处理无扩展名的 URLs：

[multiviews]: https://httpd.apache.org/docs/current/content-negotiation.html#multiviews

{% highlight apache %}
Options +MultiViews
{% endhighlight %}

### Nginx

[try_files][] 指令允许你指定一个文件列表搜索，用来处理请求。如果请求的 URL 的精确匹配未找到的的话，下列配置会让 nginx 搜索含有 `.html` 扩展名的文件。

[try_files]: http://nginx.org/en/docs/http/ngx_http_core_module.html#try_files

{% highlight nginx %}
try_files $uri $uri.html $uri/ =404;
{% endhighlight %}
