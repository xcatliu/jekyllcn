---
layout: docs
title: 资源
permalink: /docs/assets/
translators: [yzyzsun, LeuisKen, TimoTokki]
update_date: 2016-04-26
hash: 5647b91
---

Jekyll 提供了对 Sass 的内建支持，还能通过安装相应的 Ruby gem 支持 CoffeeScript。使用时只需创建以 `.sass`、`.scss` 或 `.coffee` 为扩展名的文件，***并以两行 `---` 开头即可***，例如：

{% highlight sass %}
---
---

// start content
.my-definition
  font-size: 1.2em
{% endhighlight %}

Jekyll 将这些文件的输出存放在同一目录下，例如网站源目录下的 `css/styles.scss`，Jekyll 会处理生成网站目标目录下的 `css/styles.css`。

<div class="note info">
  <h5>Jekyll 会处理 asset 文件中的所有 Liquid 过滤器和标签</h5>
  <p>如果你在使用 <a href="http://mustache.github.io">Mustache</a> 或其他会与 <a href="/docs/templates/">Liquid 模板语法</a> 冲突的 JavaScript 模板语言，那么你需要将你的代码放在 <code>{&#37; raw &#37;}</code> 和 <code>{&#37; endraw &#37;}</code> 标签内。</p>
</div>

## Sass/SCSS

Jekyll 允许在某些方面自定义 Sass 转换。

你需要将所有需要导入的部分文件放在 `sass_dir` 下，该路径默认是 `<source>/_sass`；而主 SCSS / Sass 文件放在你希望输出文件所在的目录下，如 `<source>/css`。详情可以参考 [示例网站][example-sass]。

如果你在使用 Sass 的 `@import` 语句，则需要确保你的 `sass_dir` 已设为 Sass 文件所在的目录。你可以这样设置：

{% highlight yaml %}
sass:
    sass_dir: _sass
{% endhighlight %}

Sass 转换器默认配置中的 `sass_dir` 为 `_sass`。

[example-sass]: https://github.com/jekyll/jekyll-sass-converter/tree/master/example

<div class="note info">
  <h5><code>sass_dir</code> 只用于 Sass</h5>
  <p>

    注意 <code>sass_dir</code> 只是 Sass 的导入目录，没有其他作用。这意味着 Jekyll 并不直接知晓这些文件，所以这里的文件不应该包含 YAML 头信息，它们亦不会被转换。该目录只应该包含导入文件。

  </p>
</div>

你也可以在 `_config.yml` 的 `style` 选项中指定输出样式：

{% highlight yaml %}
sass:
    style: compressed
{% endhighlight %}

这些设置将传递给 Sass，因此所有 Sass 支持的输出样式在这里都可以使用。

## Coffeescript

为了确保 Coffeescript 能在 Jekyll 3.0 使用，你必须：

* 安装 `jekyll-coffeescript` gem
* 确保你的 `_config.yml` 包含下列设置并更新（即重新 `jekyll serve`）：

{% highlight yaml %}
gems:
 - jekyll-coffeescript
{% endhighlight %}


