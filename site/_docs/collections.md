---
layout: docs
title: 集合（Collections）
permalink: /docs/collections/
translators: [LeuisKen, TimoTokki]
update_date: 2016-04-26
---

并非所有的都会是文章或页面。也许您想要记录您开源项目中涉及的各种解决方案，团队成员，或是某次会议记录。集合（Collection）允许您定义一种新的文档类型，它既可以像页面和文章那样工作，也可以拥有它们特有的属性和命名空间。

## 使用集合

### 第一步：让 Jekyll 读取您的集合

将下面的代码加入您的 `_config.yml` 文件，将 `my_collection` 替换为您集合的名字。

{% highlight yaml %}
collections:
- my_collection
{% endhighlight %}

您也可以在配置中为你的集合加入具体的元数据：

{% highlight yaml %}
collections:
  my_collection:
    foo: bar
{% endhighlight %}

集合也可以设置默认的属性：

{% highlight yaml %}
defaults:
  - scope:
      path: ""
      type: my_collection
    values:
      layout: page
{% endhighlight %}

### 第二步：加入您的内容

创建对应的文件夹（如 `<source>/_my_collection`）并添加文件。若 YAML 头信息存在，他将被作为数据读入，并且其后的任何信息都将被保存在文档的`content` 属性中。如果没有任何 YAML 头信息存在， Jekyll 将不会在您的集合中生成任何文件。

<div class="note info">
  <h5>确保你的文件夹命名正确</h5>
  <p>
文件夹名称必须和你在<code>_config.yml</code>中定义的集合名称完全一致，包括前缀的<code>_</code>字符。
  </p>
</div>

### 第三步：选择性渲染你的集合文件为独立文件

如果你希望 Jekyll 对每一个你集合中的文件，都创建一个公开的，渲染后的版本，请在`_config.yml`中，将你集合的元数据中将`output`键设置为`true`：

{% highlight yaml %}
collections:
  my_collection:
    output: true
{% endhighlight %}

这将会依据每一个在集合中的文档创建一个文件。例如，你有一个`_my_collection/some_subdir/some_doc.md`文件，它将利用 Liquid 以及你选用的 Markdown 转换器创建一个`<dest>/my_collection/some_subdir/some_doc.html`文件。

如同设置了 [Permalinks](../permalinks/) 属性的文章，这些文件的URL也可以通过对集合的`permalink`元数据进行设置来自定义。

{% highlight yaml %}
collections:
  my_collection:
    output: true
    permalink: /awesome/:path/
{% endhighlight %}

例如，你有一个`_my_collection/some_subdir/some_doc.md`文件，它将写入到`<dest>/awesome/some_subdir/some_doc/index.html`路径下。

<div class="note info">
  <h5>不要忘记添加 YAML 头</h5>
  <p>
  没有头信息的文件将被视为<a href="/docs/static-files">静态文件</a>，它们仅会被简单拷贝到目的路径下，而不会被处理。
  </p>
</div>

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
      <td>
        <p><code>collection</code></p>
      </td>
      <td>
        <p>所包含集合的标签</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>path</code></p>
      </td>
      <td>
        <p>文档相对于集合文件夹的路径</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>name</code></p>
      </td>
      <td>
        <p>文档的基本文件名，任何空格和非字母数字的字符将被替换为连字符</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>title</code></p>
      </td>
      <td>
        <p>文档的小写字母标题（在 <a href="/docs/frontmatter/">头信息</a>中定义），任何空格和非字母数字的字符将被替换为连字符。如果title在<a href="/docs/frontmatter/">头信息</a>中未定义，该值等同于<code>name</code>。</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>output_ext</code></p>
      </td>
      <td>
        <p>输出文件的文件扩展名</p>
      </td>
    </tr>
  </tbody>
</table>
</div>

## Liquid 属性

### 集合

每个集合均可访问 Liquid 的`site`变量。例如，若你希望获取`_albums`中的集合`albums`，请使用`site.albums`变量。每个集合都具有一个他本身的文档数组（例如，`site.albums`就是一个文档组成的数组，和`site.pages`、`site.posts`类似）。下面会介绍如何获取这些文档的属性。

集合可以通过`site.collections`获取，其中包含你在`_config.yml`（如果存在）中定义的元数据和下面的信息：

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
        <p><code>label</code></p>
      </td>
      <td>
        <p>
          你集合的名称，如<code>my_collection</code>。
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>docs</code></p>
      </td>
      <td>
        <p>
          由<a href="#documents">文档</a>构成的数组。
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>files</code></p>
      </td>
      <td>
        <p>
          由集合中静态文件构成的数组。
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>relative_directory</code></p>
      </td>
      <td>
        <p>
          集合中相对于站点路径的源目录的路径。
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>directory</code></p>
      </td>
      <td>
        <p>
          集合源目录的完整路径。
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>output</code></p>
      </td>
      <td>
        <p>

          集合中的文件将作为单独的文件输出。

        </p>
      </td>
    </tr>
  </tbody>
</table>
</div>


### 文档

作为文档 YAML 头信息的补充，每一个文档还具有以下属性。

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
      <td>
        <p><code>content</code></p>
      </td>
      <td>
        <p>
          文档的内容（未被渲染的）。若不存在 YAML 头信息， Jekyll 将不会在你的集合中生成该文件。若定义 YAML 头，这部分内容将是头信息结尾`---`后面的全部内容。
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>output</code></p>
      </td>
      <td>
        <p>
          基于文档<code>content</code>的渲染后的输出。
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>path</code></p>
      </td>
      <td>
        <p>
          文档源文件的完整路径。
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>relative_path</code></p>
      </td>
      <td>
        <p>
          文档相对于站点源的相对路径。
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>url</code></p>
      </td>
      <td>
        <p>
          渲染后集合的 URL 。该文件仅在其所属集合名称在站点配置文件中的 <code>render</code> 键中时会被写入到目的地。
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>collection</code></p>
      </td>
      <td>
        <p>
          文档所属的集合名称。
        </p>
      </td>
    </tr>
  </tbody>
</table>
</div>

## 获取集合的属性

在站点的任何位置，你都可以获取在 YAML 头重的属性。通过上面的示例，配置一个`site.albums`集合，并在对应的文件的头信息中创建如下结构的数据（需要使用引擎支持的标记语言，且不能以`.yaml`作为扩展名）：

{% highlight yaml %}
title: "Josquin: Missa De beata virgine and Missa Ave maris stella"
artist: "The Tallis Scholars"
director: "Peter Phillips"
works:
  - title: "Missa De beata virgine"
    composer: "Josquin des Prez"
    tracks:
      - title: "Kyrie"
        duration: "4:25"
      - title: "Gloria"
        duration: "9:53"
      - title: "Credo"
        duration: "9:09"
      - title: "Sanctus & Benedictus"
        duration: "7:47"
      - title: "Agnus Dei I, II & III"
        duration: "6:49"
{% endhighlight %}

若要在一个页面中列出集合中的专辑（album），可以使用下面的模板：

{% highlight html %}
{% raw %}
{% for album in site.albums %}
  <h2>{{ album.title }}</h2>
  <p>Performed by {{ album.artist }}{% if album.director %}, directed by {{ album.director }}{% endif %}</p>
  {% for work in album.works %}
    <h3>{{ work.title }}</h3>
    <p>Composed by {{ work.composer }}</p>
    <ul>
    {% for track in work.tracks %}
      <li>{{ track.title }} ({{ track.duration }})</li>
    {% endfor %}
    </ul>
  {% endfor %}
{% endfor %}
{% endraw %}
{% endhighlight %}
