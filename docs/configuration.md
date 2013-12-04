---
layout: docs
title: 配置
prev_section: structure
next_section: frontmatter
permalink: /docs/configuration/
contributor: debbbbie
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
          转换时强制包含某些文件、文件夹。 <code>.htaccess</code> 是个典型的例子，因为默认排除 . 开头的文件。
        </p>
      </td>
      <td class='align-center'>
        <p><code class="option">include: [DIR, FILE, ...]</code></p>
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
            设置文件的编码，仅 Ruby 1.9 以上可用。默认值为 nil ，使用 Ruby 默认的
             <code>ASCII-8BIT</code>。可以用命令
             <code>ruby -e 'puts Encoding::list.join("\n")'</code> 查看 Ruby 可用的编码。
        </p>
      </td>
      <td class='align-center'>
        <p><code class="option">encoding: ENCODING</code></p>
      </td>
    </tr>
  </tbody>
</table>
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
        <p class="description">手动设置配置文件，可设置多个，且后边的设置会覆盖前边的。</p>
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
  </tbody>
</table>
</div>

<div class="note warning">
  <h5>不要在配置文件中使用 tab 制表符</h5>
  <p>
    这将造成解析错误，或倒回到默认设置。请使用空格替代。
  </p>
</div>

## 默认配置

Jekyll 默认使用以下的配置：

<div class="note warning">
  <h5>有两个 kramdown 的选项不支持</h5>
  <p>
    注意 Jekyll 当前不支持 <code>remove_block_html_tags</code> 和
     <code>remove_span_html_tags</code> ，因为没有被包含到 kramdown HTML 转换器中。
  </p>
</div>

{% highlight yaml %}
source:      .
destination: ./_site
plugins:     ./_plugins
layouts:     ./_layouts
include:     ['.htaccess']
exclude:     []
keep_files:  ['.git','.svn']
timezone:    nil
encoding:    nil

future:      true
show_drafts: nil
limit_posts: 0
pygments:    true

relative_permalinks: true

permalink:     date
paginate_path: 'page:num'

markdown:      maruku
markdown_ext:  markdown,mkd,mkdn,md
textile_ext:   textile

excerpt_separator: "\n\n"

safe:        false
watch:       false    # deprecated
server:      false    # deprecated
host:        0.0.0.0
port:        4000
baseurl:     /
url:         http://localhost:4000
lsi:         false

maruku:
  use_tex:    false
  use_divs:   false
  png_engine: blahtex
  png_dir:    images/latex
  png_url:    /images/latex

rdiscount:
  extensions: []

redcarpet:
  extensions: []

kramdown:
  auto_ids: true
  footnote_nr: 1
  entity_output: as_char
  toc_levels: 1..6
  smart_quotes: lsquo,rsquo,ldquo,rdquo
  use_coderay: false

  coderay:
    coderay_wrap: div
    coderay_line_numbers: inline
    coderay_line_numbers_start: 1
    coderay_tab_width: 4
    coderay_bold_every: 10
    coderay_css: style

redcloth:
  hard_breaks: true
{% endhighlight %}


## Markdown 选项

Jekyll 支持的 Markdown 渲染器中有的有额外的选项。

### Redcarpet

Redcarpet支持设置 `extensions` ，值为一个字符串数组，每个字符串都是 `Redcarpet::Markdown` 类的扩展，相应的扩展就会设置为 `true` 。

Jekyll handles two special Redcarpet extensions:

- `no_fenced_code_blocks` --- 默认的， Jekyll 设置扩展 `fenced_code_blocks` (用三个波浪线或重音线标记代码区间) 为 `true` ，这或许是跟 GitHub 积极的采用有关。当使用Jekyll的时候， Redcarpet 的扩展 `fenced_code_blocks` 无效，作为替代方案，你可以这样做：

    注意你还可以这样来配置语言以支持语法高亮：

        ```ruby
        # ...ruby code
        ```

    有了 both fenced code blocks 和 pygments ，就会直接高亮代码了；如果没有 pygments，将增加一个 `class="LANGUAGE"` 属性到 `<code>` 元素，用于给不同的 JavaScript 代码高亮库做后续处理。
- `smart` --- 打开 SmartyPants ，将引号转为 &quot; 、连字符转为 em (`---`) 和 en (`--`) 破折号。

Redcarpet 所有其他扩展保持他们本来的名字，并且在 Jekyll 中不能给 `smart` 加渲染选项。 [Redcarpet 的 README 中有可用扩展的列表。][redcarpet_extensions] 确保你看的 README 是正确的版本： Jekyll 当前用的是 v2.2.x ，其中 `footnotes` 和 `highlight` 在 3.0.0 以后才会支持。最常用的扩展是如下：

- `tables`
- `no_intra_emphasis`
- `autolink`

[redcarpet_extensions]: https://github.com/vmg/redcarpet/blob/v2.2.2/README.markdown#and-its-like-really-simple-to-use
