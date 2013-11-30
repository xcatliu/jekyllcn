---
layout: docs
title: 永久链接
prev_section: templates
next_section: pagination
permalink: /docs/permalinks/
contributor: debbbbie
---

Jekyll 支持以灵活的方式管理你网站的链接，你可以通过 [Configuration](../configuration/) 或
 [YAML 头信息](../frontmatter/) 为每篇文章设置永久链接。你可以随心所欲的选择你自己的
 格式，即使自定义。默认配置为 `date`。

永久链接的模板用以冒号为前缀的关键词标记动态内容，比如 `date` 代表
 `/:categories/:year/:month/:day/:title.html` 。

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
        <p>文章所在文件的年份</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>month</code></p>
      </td>
      <td>
        <p>文章所在文件的月份，格式如 `01, 10` </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>i_month</code></p>
      </td>
      <td>
        <p>文章所在文件的月份，格式如 `1, 10` </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>day</code></p>
      </td>
      <td>
        <p>文章所在文件的日期，格式如 `01, 20`</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>i_day</code></p>
      </td>
      <td>
        <p>文章所在文件的日期，格式如 `1, 20`</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>title</code></p>
      </td>
      <td>
        <p>文章所在文件的标题</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>categories</code></p>
      </td>
      <td>
        <p>
          为文章配置的目录，Jekyll可以自动将 `//` 转换为 `/` ，所以如果没有目录，会自动忽略
        </p>
      </td>
    </tr>
  </tbody>
</table>
</div>

## 已经建好的链接类型

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>链接类型</th>
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
        <p><code>none</code></p>
      </td>
      <td>
        <p><code>/:categories/:title.html</code></p>
      </td>
    </tr>
  </tbody>
</table>
</div>

## 举例

比如文件名： `/2009-04-29-slap-chop.textile`

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>设置</th>
      <th>对应的 URL </th>
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
        <p><code>permalink: pretty</code></p>
      </td>
      <td>
        <p><code>/2009/04/29/slap-chop/index.html</code></p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>permalink: /:month-:day-:year/:title.html</code></p>
      </td>
      <td>
        <p><code>/04-29-2009/slap-chop.html</code></p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>permalink: /blog/:year/:month/:day/:title</code></p>
      </td>
      <td>
        <p><code>/blog/2009/04/29/slap-chop/index.html</code></p>
      </td>
    </tr>
  </tbody>
</table>
</div>
