---
layout: docs
title: 配置
permalink: /docs/configuration/
translators: [debbbbie, chaucerling, archersmind, TimoTokki, baiyangcao, MondoGao]
update_date: 2017-04-26
hash: 5647b91
---

Jekyll允许你很轻松的设计你的网站，这很大程度上归功于灵活强大的配置功能。既可以配置在网站根目录下的
 `_config.yml` 文件，也可以作为命令行的标记来配置。

## 配置设置

### 全局配置

下表中列举了所有 Jekyll 可用的设置，和多种多样的 <code class="option">选项</code> (配置文件中)
及 <code class="flag">标记</code> (命令行中)。

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>设置</th>
      <th>
        <span class="option">选项</span> 和 <span class="flag">标记</span>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Site Source</strong></p>
        <p class='description'>修改 Jekyll 读取文件的路径</p>
      </td>
      <td class="align-center">
        <p><code class="option">source: DIR</code></p>
        <p><code class="flag">-s, --source DIR</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Site Destination</strong></p>
        <p class='description'>修改 Jekyll 写入文件的路径</p>
      </td>
      <td class="align-center">
        <p><code class="option">destination: DIR</code></p>
        <p><code class="flag">-d, --destination DIR</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Safe</strong></p>
        <p class='description'>禁用 <a href="../plugins/">自定义插件</a>。</p>
      </td>
      <td class="align-center">
        <p><code class="option">safe: BOOL</code></p>
        <p><code class="flag">--safe</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Exclude</strong></p>
        <p class="description">转换时排除某些文件、文件夹</p>
      </td>
      <td class='align-center'>
        <p><code class="option">exclude: [DIR, FILE, ...]</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Include</strong></p>
        <p class="description">
          转换时强制包含某些文件、文件夹。<code>.htaccess</code> 是个典型的例子，因为默认排除 . 开头的文件。
        </p>
      </td>
      <td class='align-center'>
        <p><code class="option">include: [DIR, FILE, ...]</code></p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>Keep files</strong></p>
        <p class="description">
          当生成站点时，保留选择的文件。对文件不是由 jekyll 生成是有用的。例如由你的构建工具生成的文件或者资源。路径是相对于 <code>destination</code> 。
        </p>
      </td>
      <td class="align-center">
        <p><code class="option">keep_files: [DIR, FILE, ...]</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Time Zone</strong></p>
        <p class="description">
            设置时区，这个设置作用于 <code>TZ</code> 变量， Ruby 用它来处理日期和时间。
            <a href="http://en.wikipedia.org/wiki/Tz_database">IANA Time Zone
            Database</a> 里边的都有效，比如 <code>America/New_York</code> 。默认值为操作系统的时区。
        </p>
      </td>
      <td class='align-center'>
        <p><code class="option">timezone: TIMEZONE</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Encoding</strong></p>
        <p class="description">
            设置文件的编码，仅 Ruby 1.9 以上可用。2.0.0　版本以后默认值为 utf-8，之前版本默认值为 nil，使用 Ruby 默认的 <code>ASCII-8BIT</code>。可以用命令 <code>ruby -e 'puts Encoding::list.join("\n")'</code> 查看 Ruby 可用的编码。
        </p>
      </td>
      <td class='align-center'>
        <p><code class="option">encoding: ENCODING</code></p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>Defaults</strong></p>
        <p class='description'>
            设置 <a href="../frontmatter/" title="YAML Front Matter">YAML 头信息</a> 的默认值。
        </p>
      </td>
      <td class='align-center'>
        <p><a href="#front-matter-defaults" title="details">详细</a></p>
      </td>
    </tr>
  </tbody>
</table>
</div>

<div class="note warning">
  <h5>Destination 文件夹会在站点建立时被清理</h5>
  <p>
    <code>&lt;destination&gt;</code> 的内容默认在站点建立时会被自动清理。不是你创建的文件和文件夹会被删除。你想在 <code>&lt;destination&gt;</code> 保留的文件和文件夹应在 <code>&lt;keep_files&gt;</code> 里指定。
  </p>
  <p>
    不要把<code>&lt;destination&gt;</code> 设置到重要的路径上，而应该把它作为一个暂存区域,从那里复制文件到您的web服务器。
  </p>
</div>

### 编译选项

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>设置</th>
      <th><span class="option">选项</span> 和 <span class="flag">标记</span></th>
    </tr>
  </thead>
  <tbody>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Regeneration</strong></p>
        <p class='description'>允许文件修改时自动重新生成网站。</p>
      </td>
      <td class="align-center">
        <p><code class="flag">-w, --watch</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Configuration</strong></p>
        <p class="description">手动设置配置文件，可设置多个，且后边的配置会覆盖前边的。</p>
      </td>
      <td class='align-center'>
        <p><code class="flag">--config FILE1[,FILE2,...]</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Drafts</strong></p>
        <p class="description">处理草稿</p>
      </td>
      <td class='align-center'>
        <p><code class="flag">--drafts</code></p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>Environment</strong></p>
        <p class="description">build　时使用特定的环境变量。</p>
      </td>
      <td class="align-center">
        <p><code class="flag">JEKYLL_ENV=production</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Future</strong></p>
        <p class="description">用将来的日期发布文章</p>
      </td>
      <td class='align-center'>
        <p><code class="option">future: BOOL</code></p>
        <p><code class="flag">--future</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>LSI</strong></p>
        <p class="description">为相关文章生成索引</p>
      </td>
      <td class='align-center'>
        <p><code class="option">lsi: BOOL</code></p>
        <p><code class="flag">--lsi</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Limit Posts</strong></p>
        <p class="description">限制文章的数量</p>
      </td>
      <td class='align-center'>
        <p><code class="option">limit_posts: NUM</code></p>
        <p><code class="flag">--limit_posts NUM</code></p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>Force polling</strong></p>
        <p class="description">强制使用轮询。</p>
      </td>
      <td class="align-center">
        <p><code class="flag">--force_polling</code></p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>Verbose output</strong></p>
        <p class="description">显示详细输出。</p>
      </td>
      <td class="align-center">
        <p><code class="flag">-V, --verbose</code></p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>Silence Output</strong></p>
        <p class="description">在编译期间不显示的正常输出。</p>
      </td>
      <td class="align-center">
        <p><code class="flag">-q, --quiet</code></p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>Incremental build</strong></p>
        <p class="description">
            启用实验特性 incremental build。Incremental build 只重建修改过的 posts 和 pages，对大型网站有显著的性能提升，但在特定情况下也会影响网站生成。
        </p>
      </td>
      <td class="align-center">
        <p><code class="option">incremental: BOOL</code></p>
        <p><code class="flag">-I, --incremental</code></p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>Liquid profiler</strong></p>
        <p class="description">
            生成一个Liquid概述文档来帮助你发现性能瓶颈
        </p>
      </td>
      <td class="align-center">
        <p><code class="option">profile: BOOL</code></p>
        <p><code class="flag">--profile</code></p>
      </td>
    </tr>
  </tbody>
</table>
</div>

### 服务选项

除了下边的选项， `serve` 命令还可以接收 `build` 的选项，当运行网站服务之前的编译时候使用。

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>设置</th>
      <th><span class="option">选项</span> 和 <span class="flag">标记</span></th>
    </tr>
  </thead>
  <tbody>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Local Server Port</strong></p>
        <p class='description'>监听所给的端口</p>
      </td>
      <td class="align-center">
        <p><code class="option">port: PORT</code></p>
        <p><code class="flag">--port PORT</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Local Server Hostname</strong></p>
        <p class='description'>监听所给的主机名</p>
      </td>
      <td class="align-center">
        <p><code class="option">host: HOSTNAME</code></p>
        <p><code class="flag">--host HOSTNAME</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Base URL</strong></p>
        <p class='description'>网站的根路径</p>
      </td>
      <td class="align-center">
        <p><code class="option">baseurl: URL</code></p>
        <p><code class="flag">--baseurl URL</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Detach</strong></p>
        <p class='description'>从终端命令行中分离出来</p>
      </td>
      <td class="align-center">
        <p><code class="option">detach: BOOL</code></p>
        <p><code class="flag">-B, --detach</code></p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>Skips the initial site build.</strong></p>
        <p class="description">跳过服务器启动之前，网站的初始化。</p>
      </td>
      <td class="align-center">
        <p><code class="flag">--skip-initial-build</code></p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>X.509 (SSL) Private Key</strong></p>
        <p class="description">SSL私钥</p>
      </td>
      <td class="align-center">
        <p><code class="flag">--ssl-key</code></p>
      </td>
    </tr>
    <tr class="setting">
      <td>
        <p class="name"><strong>X.509 (SSL) Certificate</strong></p>
        <p class="description">SSL公证</p>
      </td>
      <td class="align-center">
        <p><code class="flag">--ssl-cert</code></p>
      </td>
    </tr>
  </tbody>
</table>
</div>

<div class="note warning">
  <h5>不要在配置文件中使用 tab 制表符</h5>
  <p>
    这将造成解析错误，或倒回到默认设置。请使用空格替代。
  </p>
</div>

## 自定义 WEBRick 消息头
<!-- WEBRick 为 Ruby 常用的一个 Web 服务器　-->
你可以在 `_config.yml` 中为你的站点提供自定义的 HTTP 消息头

{% highlight yaml %}
# 文件: _config.yml
webrick:
  headers:
    My-Header: My-Value
    My-Other-Header: My-Other-Value
{% endhighlight %}

### 默认消息头

Jekyll 将默认在响应中添加 `Content-Type` 和 `Cache-Control` 请求头：前者动态的匹配被请求资源的类型，后者将在开发模式下禁用缓存以让浏览器强制获取到最新的资源版本。

## 指定 Jekyll 构建时的环境变量

在 build（或 serve）命令参数中，你可以指定 Jekyll 的环境变量。然后 build 命令会将该环境变量暴露在给 `jekyll.environment` 变量以便于在代码中做环境判断。

假设在你的代码中存在如下的判断语句：

{% highlight liquid %}
{% raw %}
{% if jekyll.environment == "production" %}
   {% include disqus.html %}
{% endif %}
{% endraw %}
{% endhighlight %}

当在构建你的 Jekyll 网站时，if 语句块中的内容不会被执行；除非你在 build 命令中还像下文这样指定了一个 `production` 环境：

{% highlight sh %}
JEKYLL_ENV=production jekyll build
{% endhighlight %}

设置环境变量允许你只在特定环境下执行指定内容。

`JEKYLL_ENV` 的默认值是 `development`。因此，如果你在 build 参数中省略 `JEKYLL_ENV`，那么默认为 `JEKYLL_ENV=development`。任何 `{% raw %}{% if jekyll.environment == "development" %}{% endraw %}` 中的内容在 build 时都会自动显现。

你的环境参数可以任意设置（不止是 `development` 或者 `production` ）。你可能想在开发环境下隐藏一些元素，比如外部评论功能或谷歌分析插件；或是在开发环境中增加一个“在 GitHub中编辑”的按钮，但却不让其在生产环境中显示。

在 build 命令中指定参数，当你迁移环境时，可以避免更改你配置文件中的值。

## 头信息默认值

通过使用 [YAML 头信息](../frontmatter/)可以指定站点的页面和文章的配置。设置一些东西例如布局或者自定义标题，亦或是给文章指定一个更精确的日期/时间，这都可以往页面或文章的头信息添加数据来实现。

很多时候，你会发现你在重复填写很多配置项。在每个文件里设置相同的布局，对每篇文章添加相同的分类，等等。你甚至可能添加自定义变量，如作者名，这可能对你博客上大部分的文章来说是相同的。

Jekyll 提供了一个方法在站点配置中设置这些默认值，而不是在每次创建一个新的文章或页面重复此配置。要做到这一点，你可以在项目根目录下的 `_config.yml` 文件里设置 `defaults` 的值指定全站范围的默认值。

`defaults` 保存一个范围/值的对的数组，这定义了哪些默认值要设置到一个特定的文件路径下的文件，或者可选的，在该路径下指定 的文件类型的文件。

假设您想添加一个默认的布局给站点中的所有页面和文章。 你要将这添加到你的 `_config.yml` 文件：

{% highlight yaml %}
defaults:
  -
    scope:
      path: "" # 一个空的字符串代表项目中所有的文件
    values:
      layout: "default"
{% endhighlight %}

<div class="note info">
  <h5>请重新运行命令： `jekyll serve` </h5>
  <p>
    主要配置文件 <code>_config.yml</code> 包括一些在运行时一次性读入的全局配置和变量定义，
    在自动生成的过程中并不会重新加载 <code>_config.yml</code> 文件所发生的改变，除非重新运行。
  </p>
  <p>
    注意 <a href="../datafiles">Data Files</a> 包括在自动生成范围内，可以在更改后自动重新加载。
  </p>
</div>

在这里，我们把 `values` 应用给 scope 路径里的所有文件。因为路径被设为空字符串，它将会应用到你项目里的**全部文件**。你可能不想给项目在的每个文件都设置一个布局，例如 css 文件，所以你可以在 `scope` 下指定 `type` 的值。

{% highlight yaml %}
defaults:
  -
    scope:
      path: "" # 一个空的字符串代表项目中所有的文件
      type: "posts" # 以前的 `post`， 在 Jekyll 2.2 里。
    values:
      layout: "default"
{% endhighlight %}

现在，这只会给类型是 `posts` 的文件设置默认布局。你可以使用的不同的类型分别是 `pages` ， `posts` ，  `drafts` 或者其他你站点中的集合。当创建一个范围/值的对，如果选择了 `type`，你必须指定一个值给 `path` 。

正如前面所提到的，您可以给 `defaults` 设置多个范围/值的对。

{% highlight yaml %}
defaults:
  -
    scope:
      path: ""
      type: "posts"
    values:
      layout: "my-site"
  -
    scope:
      path: "projects"
      type: "pages" # 以前的 `page`， 在 Jekyll 2.2 里。
    values:
      layout: "project" # 覆盖之前的默认布局
      author: "Mr. Hyde"
{% endhighlight %}

有了这些默认值，所有的文章都会使用 `my-site` 布局。任何在 `projects/` 文件夹下的 html 文件会使用 `project` 布局。这些文件也会拥有值为 `Mr. Hyde` 的 `page.author` 这一 [liquid 变量](../variables/)，同时这些页面的类别被设为 `project` 。

{% highlight yaml %}
collections:
  - my_collection:
    output: true

defaults:
  -
    scope:
      path: ""
      type: "my_collection" # 你的站点里的一个集合，复数形式
    values:
      layout: "default"
{% endhighlight %}

在这个例子中，在 [collection](../collections/) 里面 `layout` 被设为 `default` ，用 `my_collection` 的名字。

### 优先权

Jekyll 会应用你在 `_config.yml` 文件里 `defaults` 部分的所有配置设定。然而，你可以选择
覆盖这些设定，通过在范围/值的对里指定一个更具体的路径。

你可以观察上一个例子。一开始我们设置了 `my-site` 这一默认的布局。然后，使用一个更具体的路径，
我们把在 `projects/` 路径下的文件的默认布局设置为 `project` 。这可以使用你想在页面或者文章的头信息里设定的任意值来达成。

最后，如果你在 `_config.yml` 的 `defaults` 部分设置了站点的默认值，你可以在页面或文章的文件里覆盖这些设定。你需要做的是在在页面或文章的头信息里指定要覆盖的设定。例如：

{% highlight yaml %}
# In _config.yml
...
defaults:
  -
    scope:
      path: "projects"
      type: "pages"
    values:
      layout: "project"
      author: "Mr. Hyde"
      category: "project"
...
{% endhighlight %}

{% highlight yaml %}
# In projects/foo_project.md
---
author: "John Smith"
layout: "foobar"
---
The post text goes here...
{% endhighlight %}

在站点建立时 `projects/foo_project.md` 的布局会是 `foobar`而不是`project` ， `author` 是 `John Smith`而不是 `Mr. Hyde` 。

## 默认配置

Jekyll 默认使用以下的配置运行。也可以在配置文件或者命令行中显示地指定这些选项。

<div class="note warning">
  <h5>有两个 kramdown 的选项不支持</h5>
  <p>
    注意 Jekyll 当前不支持 <code>remove_block_html_tags</code> 和
     <code>remove_span_html_tags</code> ，因为没有被包含到 kramdown HTML 转换器中。
  </p>
</div>

{% highlight yaml %}
# 目录结构
source:      .
destination: ./_site
plugins:     ./_plugins
layouts:     ./_layouts
data_source: ./_data
collections: null

# 阅读处理
safe:         false
include:      [".htaccess"]
exclude:      []
keep_files:   [".git", ".svn"]
encoding:     "utf-8"
markdown_ext: "markdown,mkdown,mkdn,mkd,md"

# 内容过滤
show_drafts: null
limit_posts: 0
future:      true
unpublished: false

# 插件
whitelist: []
gems:      []

# 转换
markdown:    kramdown
highlighter: rouge
lsi:         false
excerpt_separator: "\n\n"
incremental: false

# 服务器选项
detach:  false
port:    4000
host:    127.0.0.1
baseurl: "" # does not include hostname

# 输出
permalink:     date
paginate_path: /page:num
timezone:      null

quiet:    false
defaults: []

# Markdown 处理器
rdiscount:
  extensions: []

redcarpet:
  extensions: []

kramdown:
  auto_ids:       true
  footnote_nr:    1
  entity_output:  as_char
  toc_levels:     1..6
  smart_quotes:   lsquo,rsquo,ldquo,rdquo
  enable_coderay: false

  coderay:
    coderay_wrap:              div
    coderay_line_numbers:      inline
    coderay_line_number_start: 1
    coderay_tab_width:         4
    coderay_bold_every:        10
    coderay_css:               style
{% endhighlight %}

## Liquid 选项

Liquid的错误处理方式可以通过 <code>error_mode</code> 来配置，可选项有：

 - `lax` --- 忽略所有错误
 - `warn` --- 针对每个错误在控制台中输出警告信息
 - `strict` --- 输出错误信息并停止构建过程

## Markdown 选项

Jekyll 支持的 Markdown 渲染器中有的有额外的选项。

### Redcarpet

Redcarpet支持设置 `extensions` ，值为一个字符串数组，每个字符串都是 `Redcarpet::Markdown` 类的扩展，相应的扩展就会设置为 `true` 。

Jekyll 处理两个特别的 Redcarpet 扩展：

- `no_fenced_code_blocks` --- 默认的， Jekyll 设置扩展 `fenced_code_blocks` (用三个波浪线或重音线标记代码区间) 为 `true` ，这或许是跟 GitHub 积极的采用有关。当使用Jekyll的时候， Redcarpet 的扩展 `fenced_code_blocks` 无效，作为替代方案，你可以使用这个语义相反的扩展来禁用 fenced code 。

注意你还可以这样来配置语言以支持语法高亮：

        ```ruby
        # ...ruby code
        ```
    
有了 fenced code blocks 和 highlighter enabled，就会静态地高亮代码了；如果没有任何高亮语法 syntax hightlighter，将增加一个 `class="LANGUAGE"` 属性到 `<code>` 元素，用于给不同的 JavaScript 代码高亮库做为提示。

- `smart` --- 这个伪扩展pseudo-extension会打开 SmartyPants ，将引号转为 &quot; 、连字符转为 em (`---`) 和 en (`--`) 破折号。

Redcarpet 所有其他扩展保持他们本来的名字，并且在 Jekyll 中不能给 `smart` 加渲染选项。 [Redcarpet 的 README 中有可用扩展的列表。][redcarpet_extensions] 确保你看的 README 是正确的版本：Jekyll 当前用的是 v3.2.x。最常用的扩展是如下：

- `tables`
- `no_intra_emphasis`
- `autolink`

[redcarpet_extensions]: https://github.com/vmg/redcarpet/blob/v3.2.2/README.markdown#and-its-like-really-simple-to-use

### Kramdown

除了上面提到的默认值，你可以打开 Github Flavored Markdown 的识别，通过输入一个 值为 "GFM" 的 `input` 选项。

例如，在你的 `_config.yml` 中：

    kramdown:
      input: GFM

### 自定义 Markdown 处理器

如果你对创建一个自定义 Markdown 处理器感兴趣，你真的很幸运！在 `Jekyll::Converters::Markdown` 的命名空间下新建一个类：

{% highlight ruby %}
class Jekyll::Converters::Markdown::MyCustomProcessor
  def initialize(config)
    require 'funky_markdown'
    @config = config
  rescue LoadError
    STDERR.puts 'You are missing a library required for Markdown. Please run:'
    STDERR.puts '  $ [sudo] gem install funky_markdown'
    raise FatalException.new("Missing dependency: funky_markdown")
  end

  def convert(content)
    ::FunkyMarkdown.new(content).convert
  end
end
{% endhighlight %}

一旦你建立了你的类，并且它作为一个插件被正确安装到 `_plugins` 文件夹 或者 作为 gem 被正确安装，你要在你的 `_config.yml` 里指定它：

{% highlight yaml %}
markdown: MyCustomProcessor
{% endhighlight %}

## Incremental Regeneration

<div class="note warning">
  <h5>Incremental regeneration 依旧是一个实验特性</h5>
  <p>
    incremental regeneration 在大多数情况下可以工作，但不可能在所有情况下都能够正常工作。请一定小心使用该特性，报告任何未列出在下边的问题。<a href="https://github.com/jekyll/jekyll/issues/new">opening an issue on GitHub</a>. 
  </p>
</div>

Incremental regeneration 只加载更新过的文件和页面来帮助缩短 build 时间。这是通过对文件修改次数和 `.jekyll-metadata` 文件中的依赖关系的追踪实现的。

在目前的实现中，incremental regeneration 会更新一个文件或者页面，仅当它或它其中之一的依赖被修改时。现今，被追踪的依赖类型仅有 includes（{% raw %}`{% include %}`{% endraw %} 标签）和 layouts。这意味着对其它文件的 plain　references（例如，在博客列表页面中常见的 `site.posts` 递归）不会被检测为依赖。

为了补救其中一些缺陷，在文件的头信息中添加 `regenerate: true` 会强迫 Jekyll 重建文件，不管文件是否被修改。注意这样做仅重建指定文件；指向其它文件内容的 references 不会起作用，因为它们不会被再次执行。

Incremental regeneration 可以在命令行中经由 `--incremental` flag（简写为 `-I`）启用，或者在配置文件中写入 `incremental: true` 启用。
