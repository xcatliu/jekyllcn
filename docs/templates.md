---
layout: docs
title: 模板
prev_section: migrations
next_section: permalinks
permalink: /docs/templates/
contributor: debbbbie
---

Jekyll 使用 [Liquid](http://wiki.shopify.com/Liquid)模板语言，支持所有标准的
 Liquid [标签](http://wiki.shopify.com/Logic) 和 [过滤器](http://wiki.shopify.com/Filters) 。
 Jekyll 甚至增加了几个过滤器和标签，方便使用。

## 过滤器

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>描述</th>
      <th><span class="filter">过滤器</span> 和 <span class="output">输出</span></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p class='name'><strong>日期转化为 XML 模式</strong></p>
        <p>将日期转化为 XML 模式 (ISO 8601) 的格式。</p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ site.time | date_to_xmlschema }}{% endraw %}</code>
        </p>
        <p>
          <code class='output'>2008-11-17T13:07:54-08:00</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>日期转化为 RFC-822 格式</strong></p>
        <p>将日期转化为 RFC-822 格式，用于 RSS 订阅。</p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ site.time | date_to_rfc822 }}{% endraw %}</code>
        </p>
        <p>
          <code class='output'>Mon, 17 Nov 2008 13:07:54 -0800</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>日期转化为短格式</strong></p>
        <p>将日期转化为短格式。</p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ site.time | date_to_string }}{% endraw %}</code>
        </p>
        <p>
          <code class='output'>17 Nov 2008</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>日期转化为长格式</strong></p>
        <p>将日期转化为长格式。</p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ site.time | date_to_long_string }}{% endraw %}</code>
        </p>
        <p>
          <code class='output'>17 November 2008</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>XML 转码</strong></p>
        <p>对一些字符串转码，已方便显示在 XML 。</p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ page.content | xml_escape }}{% endraw %}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>CGI 转码</strong></p>
        <p>
          CGI 转码，用于 URL 中，将所有的特殊字符转化为 %XX 的形式。
        </p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ “foo,bar;baz?” | cgi_escape }}{% endraw %}</code>
        </p>
        <p>
          <code class='output'>foo%2Cbar%3Bbaz%3F</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>URI 转码</strong></p>
        <p>
          URI 转码。
        </p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ “'foo, bar \\baz?'” | uri_escape }}{% endraw %}</code>
        </p>
        <p>
          <code class='output'>foo,%20bar%20%5Cbaz?</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>统计字数</strong></p>
        <p>统计文章中的字数。</p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ page.content | number_of_words }}{% endraw %}</code>
        </p>
        <p>
          <code class='output'>1337</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>数组转换为句子</strong></p>
        <p>将数组转换为句子，列举标签时尤其有用。</p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ page.tags | array_to_sentence_string }}{% endraw %}</code>
        </p>
        <p>
          <code class='output'>foo, bar, and baz</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>Textile 支持</strong></p>
        <p>将 Textile 格式的字符串转换为 HTML ，使用 RedCloth</p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ page.excerpt | textilize }}{% endraw %}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>Markdown 支持</strong></p>
        <p>将 Markdown 格式的字符串转换为 HTML 。</p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ page.excerpt | markdownify }}{% endraw %}</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>
</div>

## 标签

### 引用

如果你需要在多个地方引用一小代码片段，可以使用 `include` 标签。

{% highlight ruby %}
{% raw %}{% include footer.html %}{% endraw %}
{% endhighlight %}

Jekyll 要求所有被引用的文件放在根目录的 `_includes` 文件夹，上述代码将把
 `<source>/_includes/footer.html` 的内容包含进来。

你还可以传递参数：

{% highlight ruby %}
{% raw %}{% include footer.html param="value" %}{% endraw %}
{% endhighlight %}

这些变量可以通过 Lquid 调用：

{% highlight ruby %}
{% raw %}{{ include.param }}{% endraw %}
{% endhighlight %}

### Code snippet highlighting

Jekyll 已经支持 [超过 100 种语言](http://pygments.org/languages/) 代码高亮显示，在此感谢
 [Pygments](http://pygments.org/) 。要使用 Pygments ，你必须安装 Python 并且在配置文件
中设置 `pygments` 为 `true` 。

使用代码高亮的例子如下：

{% highlight text %}
{% raw %}
{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}
{% endraw %}
{% endhighlight %}

`highlight` 的参数 (本例中的 `ruby`) 是识别所用语言，要使用合适的识别器可以参照
 [Lexers 页](http://pygments.org/docs/lexers/) 的 “short name” 。

#### 行号

`highlight` 的第二个可选参数是 `linenos` ，使用了 `linenos`会强制在代码上加入行号。例如：

{% highlight text %}
{% raw %}
{% highlight ruby linenos %}
def foo
  puts 'foo'
end
{% endhighlight %}
{% endraw %}
{% endhighlight %}

#### 代码高亮的样式

要使用代码高亮，你还需要包含一个样式。例如你可以在
[syntax.css](http://github.com/mojombo/tpw/tree/master/css/syntax.css) 找到，这里有
跟 GitHub 一样的样式，并且免费。如果你使用了 `linenos` ，可能还需要在 `syntax.css` 加入
 `.lineno` 样式。

### Post URL

如果你想使用你某篇文章的链接，标签 `post_url` 可以满足你的需求。

{% highlight text %}
{% raw %}
{% post_url 2010-07-21-name-of-post %}
{% endraw %}
{% endhighlight %}

当使用`post_url`标签时，不需要写文件后缀名。

还可以用 Markdown 这样为你的文章生成超链接：

{% highlight text %}
{% raw %}
[Name of Link]({% post_url 2010-07-21-name-of-post %})
{% endraw %}
{% endhighlight %}

### Gist

使用 `gist` 标签可以轻松的把 GitHub Gist 签入到网站中：

{% highlight text %}
{% raw %}
{% gist 5555251 %}
{% endraw %}
{% endhighlight %}

你还可以配置 gist 的文件名，用以显示：

{% highlight text %}
{% raw %}
{% gist 5555251 result.md %}
{% endraw %}
{% endhighlight %}

`gist` 同样支持私有的 gists ，这需要 gist 所属的 github 用户名：

{% highlight text %}
{% raw %}
{% gist parkr/931c1c8d465a04042403 %}
{% endraw %}
{% endhighlight %}

私有的 gist 同样支持文件名。
