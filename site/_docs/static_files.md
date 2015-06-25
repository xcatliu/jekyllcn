---
layout: docs
title: 静态文件
permalink: /docs/static-files/
translators: yzyzsun
hash: 5647b91
---

除了用于渲染和转换的内容之外，我们还可以使用**静态文件**。

静态文件不包含任何 YAML 头信息，譬如图片、PDF 和其他不必渲染的内容。

它们在 Liquid 中可以通过 `site.static_files` 访问，还包括以下元数据：

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
      <td><p><code>file.path</code></p></td>
      <td><p>

        文件的相对路径

      </p></td>
    </tr>
    <tr>
      <td><p><code>file.modified_time</code></p></td>
      <td><p>

        文件的最后修改时间

      </p></td>
    </tr>
    <tr>
      <td><p><code>file.extname</code></p></td>
      <td><p>

        文件的扩展名，如 <code>image.jpg</code> 中的 <code>.jpg</code>

      </p></td>
    </tr>
  </tbody>
</table>
</div>
