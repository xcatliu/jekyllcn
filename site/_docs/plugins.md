---
layout: docs
title: 插件
permalink: /docs/plugins/
translators: [debbbbie, baiyangcao]
update_date: 2016-10-20
---

Jekyll 支持插件功能，你可以很容易的加入自己的代码。

<div class="note info">
  <h5>在 GitHub Pages 使用插件</h5>
  <p>
    <a href="http://pages.github.com/">GitHub Pages</a> 是由 Jekyll 提供技术支持的，考虑到安全因素，所有的 Pages 通过 <code>--safe</code> 选项禁用了插件功能，因此如果你的网站部署在 Github Pages ，那么你的插件不会工作。<br><br>
    不过仍然有办法发布到 GitHub Pages，你只需在本地做一些转换，并把生成好的文件上传到 Github 替代 Jekyll 就可以了。
  </p>
</div>

## 安装插件

可以使用以下三种方式安装插件：

1. 在网站根下目录建立 `_plugins` 文件夹，插件放在这里即可。 Jekyll 运行之前，会加载此目录下所有以 `*.rb` 结尾的文件。
2. 在你的`_config.yml`文件，添加一个键为`gems`的新数组，其值为你想要使用的gem插件的名字，例如：


        gems: [jekyll-coffeescript, jekyll-watch, jekyll-assets]
        # This will require each of these gems automatically.

    然后安装插件使用命令 `gem install jekyll-coffeescript jekyll-watch jekyll-assets`

3. 在 `Gemfile` 中的一个Bundler组里添加相关的插件，例如：

        group :jekyll_plugins do
          gem "my-jekyll-plugin"
          gem "another-jekyll-plugin"
        end

    然后需要从Bundler组中安装所有插件，使用命令`bundle install`


<div class="note info">
  <h5>
    <code>_plugins</code>, <code>_config.yml</code> and <code>Gemfile</code>
    可以同时使用
  </h5>
  <p>
    如果你愿意，可以在网站中同时使用上述安装插件的方法，使用一种安装方法并不会影响别的方法生效。
  </p>
</div>


通常，插件最终会被放在以下的目录中：

1. [生成器 - Generators](#generators)
2. [转换器 - Converters](#converters)
3. [命令 - Commands](#commands)
4. [标记 - Tags](#tags)
5. [钩子 - Hooks](#hooks)

## 生成器 - Generators

当你需要Jekyll根据你自己的规则来添加额外的内容时，你可以创建一个生成器。

生成器是 `Jekyll:Generator` 的子类，定义了一个 `generate` 方法，
接收一个[`Jekyll::Site`]({{ site.repository }}/blob/master/lib/jekyll/site.rb)类型的实例，
方法的返回值会被忽略。

生成器在Jekyll生成现存内容详细目录之后，网站生成之前运行，
含有YAML头信息的页面储存为[`Jekyll::Page`]({{ site.repository }}/blob/master/lib/jekyll/page.rb)实例，可以通过`site.pages`变量获取，
静态文件储存为[`Jekyll::StaticFile`]({{ site.repository }}/blob/master/lib/jekyll/static_file.rb)实例，可以通过`site.static_files`变量获取，
详情见[变量文档](/docs/variables/) 和
[`Jekyll::Site`]({{ site.repository }}/blob/master/lib/jekyll/site.rb)

比如，生成器可以为模板变量注入构建过程中计算出的变量值，在下面的例子中，
我们在生成器中为模板`reading.html`的两个变量`ongoing`和`done`赋了值：

```ruby
module Reading
  class Generator < Jekyll::Generator
    def generate(site)
      ongoing, done = Book.all.partition(&:ongoing?)

      reading = site.pages.detect {|page| page.name == 'reading.html'}
      reading.data['ongoing'] = ongoing
      reading.data['done'] = done
    end
  end
end
```

下面是一个更复杂的生成器例子，可以生成新的页面：

{% highlight ruby %}
module Jekyll

  class CategoryPage < Page
    def initialize(site, base, dir, category)
      @site = site
      @base = base
      @dir = dir
      @name = 'index.html'

      self.process(@name)
      self.read_yaml(File.join(base, '_layouts'), 'category_index.html')
      self.data['category'] = category

      category_title_prefix = site.config['category_title_prefix'] || 'Category: '
      self.data['title'] = "#{category_title_prefix}#{category}"
    end
  end

  class CategoryPageGenerator < Generator
    safe true

    def generate(site)
      if site.layouts.key? 'category_index'
        dir = site.config['category_dir'] || 'categories'
        site.categories.keys.each do |category|
          site.pages << CategoryPage.new(site, site.source, File.join(dir, category), category)
        end
      end
    end
  end

end
{% endhighlight %}

本例中，生成器在 `categories` 下生成了一系列文件。并使用布局 `category_index.html` 列出所有的文章。

生成器只需要实现一个方法：

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>Method</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>generate</code></p>
      </td>
      <td>
        <p>String output of the content being generated.</p>
      </td>
    </tr>
  </tbody>
</table>
</div>

## 转换器 - Converters

如果想使用一个新的标记语言，可以用你自己的转换器实现，Markdown 和 Textile 就是这样实现的。

<div class="note info">
  <h5>记住你的 YAML 头信息</h5>
  <p>
    Jekyll 只会转换带有 YAML 头信息的文件，即使你使用了插件也不行。
  </p>
</div>

下边的例子实现了一个转换器，他会用 `UpcaseConverter` 来转换所有以 `.upcase` 结尾的文件。

{% highlight ruby %}
module Jekyll
  class UpcaseConverter < Converter
    safe true
    priority :low

    def matches(ext)
      ext =~ /^\.upcase$/i
    end

    def output_ext(ext)
      ".html"
    end

    def convert(content)
      content.upcase
    end
  end
end
{% endhighlight %}

转换器需要最少实现以下 3 个方法：

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>方法</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>matches</code></p>
      </td>
      <td><p>
        检查文件后缀名是否是所要的，传入的参数是文件的后缀名（包括点号），接受的返回值是 <code>true</code> 或 <code>false</code> 。
      </p></td>
    </tr>
    <tr>
      <td>
        <p><code>output_ext</code></p>
      </td>
      <td><p>
        生成文件的后缀名（包括点号），通常是 <code>".html"</code>。
      </p></td>
    </tr>
    <tr>
      <td>
        <p><code>convert</code></p>
      </td>
      <td><p>
        转换逻辑，传入原始文件内容（不包含YAML头信息），返回值需要是 String 。
      </p></td>
    </tr>
  </tbody>
</table>
</div>

在上边的例子中， `UpcaseConverter#matches` 检查文件后缀名是不是 `.upcase` ;`UpcaseConverter#convert` 会处理检查成功文件的内容，即将所有的字符串变成大写；最终，保存的结果将以作为后缀名 `.html` 。


## 命令 - Commands

从2.5.0版本开始，Jekyll可以使用插件提供的子命令来扩展`jekyll`命令。
可以通过在`Gemfile`中`:jekyll_plugins`组中包括相关的插件来实现：

```ruby
group :jekyll_plugins do
  gem "my_fancy_jekyll_plugin"
end
```

每个`Command`必须是`Jekyll::Command`类的子类，而且必须要包含类方法`init_with_program`，例如：

```ruby
class MyNewCommand < Jekyll::Command
  class << self
    def init_with_program(prog)
      prog.command(:new) do |c|
        c.syntax "new [options]"
        c.description 'Create a new Jekyll site.'

        c.option 'dest', '-d DEST', 'Where the site should go.'

        c.action do |args, options|
          Jekyll::Site.new_site_at(options['dest'])
        end
      end
    end
  end
end
```

命令应该实现这个单例方法：

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>方法</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>init_with_program</code></p>
      </td>
      <td><p>
        这个方法接受一个参数，
        <code><a href="https://github.com/jekyll/mercenary#readme">Mercenary::Program</a></code>
        实例，表示Jekyll程序本身，程序之上，命令可以通过上述方式创建，详情可以参见Github.com上的Mercenary库。
      </p></td>
    </tr>
  </tbody>
</table>
</div>

## 标记 - Tags

如果你想使用 liquid 标记，你可以这样做。 Jekyll 官方的例子有 `highlight` 和 `include` 等标记。下边的例子中，自定义了一个 liquid 标记，用来输出当前时间：

{% highlight ruby %}
module Jekyll
  class RenderTimeTag < Liquid::Tag

    def initialize(tag_name, text, tokens)
      super
      @text = text
    end

    def render(context)
      "#{@text} #{Time.now}"
    end
  end
end

Liquid::Template.register_tag('render_time', Jekyll::RenderTimeTag)
{% endhighlight %}

liquid 标记最少需要实现如下方法：

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>方法</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>render</code></p>
      </td>
      <td>
        <p>输出标记的内容。</p>
      </td>
    </tr>
  </tbody>
</table>
</div>

你必须同时用 Liquid 模板引擎注册自定义标记，比如：

{% highlight ruby %}
Liquid::Template.register_tag('render_time', Jekyll::RenderTimeTag)
{% endhighlight %}

对于上边的例子，你可以把如下标记放在页面的任何位置：

{% highlight ruby %}
{% raw %}
<p>{% render_time page rendered at: %}</p>
{% endraw %}
{% endhighlight %}

我们在页面上会得到如下内容：

{% highlight html %}
<p>page rendered at: Tue June 22 23:38:47 –0500 2010</p>
{% endhighlight %}

### Liquid 过滤器

你可以像上边那样在 Liquid 模板中加入自己的过滤器。过滤器会把自己的方法暴露给 liquid。所有的方法都必须至少接收一个参数，用来传输入内容；返回值是过滤的结果。

{% highlight ruby %}
module Jekyll
  module AssetFilter
    def asset_url(input)
      "http://www.example.com/#{input}?#{Time.now.to_i}"
    end
  end
end

Liquid::Template.register_filter(Jekyll::AssetFilter)
{% endhighlight %}

<div class="note">
  <h5>提示™：用 Liquid 访问 site 对象</h5>
  <p>
    Jekyll 允许通过 Liquid 的<code>context.registers</code> 特性来访问 <code>site</code> 对象。比如可以用 <code>context.registers.config</code> 访问配置文件 <code>_config.yml</code> 。
  </p>
</div>

### Flags

当写插件时，有两个标记需要注意：

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>标记</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>safe</code></p>
      </td>
      <td>
        <p>
          告诉 Jekyll 此插件是否可以安全的执行任意代码。 GitHub Pages 用他来决定那个插件可以使用，哪些不可以使用。如果你的插件不允许执行任意代码，把它设为 <code>true</code> 即可。 GitHub Pages 仍然不会加载你的插件，但是如果你把他夹杂到核心中，最后保证此值设置的正确！
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>priority</code></p>
      </td>
      <td>
        <p>
          此标记决定加载插件的顺序。可以是这些值：<code>:lowest</code>, <code>:low</code>, <code>:normal</code>, <code>:high</code>, 还有 <code>:highest</code>。优先级高的先执行，优先级低的后执行。
        </p>
      </td>
    </tr>
  </tbody>
</table>
</div>

以上边例子的插件为例，应该这样设置这两个标记：

{% highlight ruby %}
module Jekyll
  class UpcaseConverter < Converter
    safe true
    priority :low
    ...
  end
end
{% endhighlight %}


## 钩子 - Hooks

通过使用钩子，你的插件可以精细控制构建过程中的各个方面。
如果你的插件定义了钩子，Jekyll就会在预定义时调用钩子。

钩子需要注册一个容器名称和事件名称，可以使用 Jekyll::Hooks.register 来注册，
传递一个容器名称、事件名称，以及钩子触发时调用的代码。
比如，假设你想要在 Jekyll 每次渲染博客时执行一些自定义的功能代码，你可以这样注册钩子：

```ruby
Jekyll::Hooks.register :posts, :post_render do |post|
  # Jekyll 渲染博客后要调用的代码
end
```

Jekyll 分别为 <code>:site</code>，<code>:pages</code>，<code>:posts</code>和 <code>:documents</code> 提供了钩子。
在任何情况下，Jekyll 都会以容器对象作为第一个回调参数来调用你的钩子，
但是所有的 `:pre_render`，`:site, :post_render`钩子都会提供一个负载哈希值作为第二个参数。
如果是 `:pre_render`，负载可以让你完全掌控渲染过程中的变量。
若是 `:site, :pre_render`，负载包括渲染所有网站的最后值（可以用于站点地图，订阅等）

完整的钩子列表如下：

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>容器名</th>
      <th>事件名</th>
      <th>调用时机</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>:site</code></p>
      </td>
      <td>
        <p><code>:after_init</code></p>
      </td>
      <td>
        <p> 在网站初始化时，但是在设置和渲染之前，适合用来修改网站的配置项</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>:site</code></p>
      </td>
      <td>
        <p><code>:after_reset</code></p>
      </td>
      <td>
        <p>网站重置之后</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>:site</code></p>
      </td>
      <td>
        <p><code>:post_read</code></p>
      </td>
      <td>
        <p>在网站数据从磁盘中读取并加载之后</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>:site</code></p>
      </td>
      <td>
        <p><code>:pre_render</code></p>
      </td>
      <td>
        <p>在渲染整个网站之前</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>:site</code></p>
      </td>
      <td>
        <p><code>:post_render</code></p>
      </td>
      <td>
        <p>在渲染整个网站之后，但是在写入任何文件之前</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>:site</code></p>
      </td>
      <td>
        <p><code>:post_write</code></p>
      </td>
      <td>
        <p>在将整个网站写入磁盘之后</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>:pages</code></p>
      </td>
      <td>
        <p><code>:post_init</code></p>
      </td>
      <td>
        <p>每次页面被初始化的时候</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>:pages</code></p>
      </td>
      <td>
        <p><code>:pre_render</code></p>
      </td>
      <td>
        <p>在渲染页面之前</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>:pages</code></p>
      </td>
      <td>
        <p><code>:post_render</code></p>
      </td>
      <td>
        <p>在页面渲染之后，但是在页面写入磁盘之前</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>:pages</code></p>
      </td>
      <td>
        <p><code>:post_write</code></p>
      </td>
      <td>
        <p>在页面写入磁盘之后</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>:posts</code></p>
      </td>
      <td>
        <p><code>:post_init</code></p>
      </td>
      <td>
        <p>每次博客被初始化的时候</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>:posts</code></p>
      </td>
      <td>
        <p><code>:pre_render</code></p>
      </td>
      <td>
        <p>在博客被渲染之前</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>:posts</code></p>
      </td>
      <td>
        <p><code>:post_render</code></p>
      </td>
      <td>
        <p>在博客渲染之后，但是在被写入磁盘之前</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>:posts</code></p>
      </td>
      <td>
        <p><code>:post_write</code></p>
      </td>
      <td>
        <p>在博客被写入磁盘之后</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>:documents</code></p>
      </td>
      <td>
        <p><code>:post_init</code></p>
      </td>
      <td>
        <p>每次文档被初始化的时候</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>:documents</code></p>
      </td>
      <td>
        <p><code>:pre_render</code></p>
      </td>
      <td>
        <p>在渲染文档之前</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>:documents</code></p>
      </td>
      <td>
        <p><code>:post_render</code></p>
      </td>
      <td>
        <p>在渲染文档之后，但是在被写入磁盘之前</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>:documents</code></p>
      </td>
      <td>
        <p><code>:post_write</code></p>
      </td>
      <td>
        <p>在文档被写入磁盘之后</p>
      </td>
    </tr>
  </tbody>
</table>
</div>

## 可用的插件

下边的插件，你可以按需索取：

#### 生成器

- [ArchiveGenerator by Ilkka Laukkanen](https://gist.github.com/707909)：用[这里的方法](https://gist.github.com/707020)生成档案。
- [LESS.js Generator by Andy Fowler](https://gist.github.com/642739)：生成的时候产生 LESS.js 文件。
- [Version Reporter by Blake Smith](https://gist.github.com/449491)：创建包含 Jekyll 版本的文件 version.html 。
- [Sitemap.xml Generator by Michael Levin](https://github.com/kinnetica/jekyll-plugins)：遍历所有的页面和文章，生成 sitemap.xml 。
- [Full-text search by Pascal Widdershoven](https://github.com/PascalW/jekyll_indextank)：全文搜索。
- [AliasGenerator by Thomas Mango](https://github.com/tsmango/jekyll_alias_generator)：根据YAML头信息中的 alias　生成跳转页面。
- [Pageless Redirect Generator by Nick Quinlan](https://github.com/nquinlan/jekyll-pageless-redirects)：根据 Jekyll 跟路径做出跳转，支持分布式。
- [Projectlist by Frederic Hemberger](https://github.com/fhemberger/jekyll-projectlist)：一个文件夹生成一个页面
- [RssGenerator by Assaf Gelber](https://github.com/agelber/jekyll-rss)：自动生成 RSS 2.0 。

#### 转换器

- [Jade plugin by John Papandriopoulos](https://github.com/snappylabs/jade-jekyll-plugin)： Jade 转换器。
- [HAML plugin by Sam Z](https://gist.github.com/517556): HAML转换器。
- [HAML-Sass Converter by Adam Pearson](https://gist.github.com/481456): HAML-Sass 转换器。 [Fork](https://gist.github.com/528642) by Sam X.
- [Sass SCSS Converter by Mark Wolfe](https://gist.github.com/960150)：在Sam X 的基础上，一个兼容 CSS 的 Sass 转换器。
- [LESS Converter by Jason Graham](https://gist.github.com/639920): 将 LESS 转换为 CSS。
- [LESS Converter by Josh Brown](https://gist.github.com/760265): 简单的 LESS 转换器。
- [Upcase Converter by Blake Smith](https://gist.github.com/449463): 一个例子 。
- [CoffeeScript Converter by phaer](https://gist.github.com/959938): [CoffeeScript](http://coffeescript.org) 转换到 JavaScript 。
- [Markdown References by Olov Lassus](https://github.com/olov/jekyll-references): 记录所有的超链接到 \_references.md 文件。
- [Stylus Converter](https://gist.github.com/988201): 将 .styl 转换为 .css 。
- [ReStructuredText Converter](https://github.com/xdissent/jekyll-rst): 用 Pygments 语法将 ReST 文档转换为 HTML 。
- [Jekyll-pandoc-plugin](https://github.com/dsanson/jekyll-pandoc-plugin): 用 pandoc 转换 markdown 。
- [Jekyll-pandoc-multiple-formats](https://github.com/fauno/jekyll-pandoc-multiple-formats) by [edsl](https://github.com/edsl):用 pandoc 生成网站，支持多种格式，并支持 pandoc 的后缀名。
- [ReStructuredText Converter](https://github.com/xdissent/jekyll-rst): 又一个用 Pygments 语法将 ReST 文档转换为 HTML 。
- [Transform Layouts](https://gist.github.com/1472645): 允许使用 HAML 布局（需要 HAML 转换器的配合）

#### 过滤器

- [Truncate HTML](https://github.com/MattHall/truncatehtml) by [Matt Hall](http://codebeef.com): 为保持 markup 结构，删除 HTML 标签。
- [Domain Name Filter by Lawrence Woodman](https://github.com/LawrenceWoodman/domain_name-liquid_filter): 过滤出域名。
- [Summarize Filter by Mathieu Arnold](https://gist.github.com/731597): 去掉 `<div id="extended">` 后边的内容。
- [URL encoding by James An](https://gist.github.com/919275):为地址编码，如 `' ' #=> '%20'` 。
- [JSON Filter](https://gist.github.com/1850654) by [joelverhagen](https://github.com/joelverhagen): 转换为 JSON 格式。
- [i18n_filter](https://github.com/gacha/gacha.id.lv/blob/master/_plugins/i18n_filter.rb):实现了 I18n 国际化的 Liquid 过滤器。
- [Smilify](https://github.com/SaswatPadhi/jekyll_smilify) by [SaswatPadhi](https://github.com/SaswatPadhi): 将表情符号转换为表情图片 ([例子](http://saswatpadhi.github.com/))。
- [Read in X Minutes](https://gist.github.com/zachleat/5792681) by [zachleat](https://github.com/zachleat): 估计读完文章需要的时间。
- [Jekyll-timeago](https://github.com/markets/jekyll-timeago): 把时间转换为 time ago 格式。
- [pluralize](https://github.com/bdesham/pluralize): 根据单词前边的数字按需转换成复数形式。
- [reading_time](https://github.com/bdesham/reading_time): 统计字数，并估计需要读的时间（已忽略HTML标签）。
- [Table of Content Generator](https://github.com/dafi/jekyll-toc-generator): 生成包含表格（ TOC ）的 HTML 代码，支持自定义。

#### 标签

- [Delicious Plugin by Christian Hellsten](https://github.com/christianhellsten/jekyll-plugins): 从 delicious.com 获取书签并展示。
- [Ultraviolet Plugin by Steve Alex](https://gist.github.com/480380): [Ultraviolet](http://ultraviolet.rubyforge.org/) 插件。
- [Tag Cloud Plugin by Ilkka Laukkanen](https://gist.github.com/710577): 生成云状的标签列表。
- [GIT Tag by Alexandre Girard](https://gist.github.com/730347): 添加 Git activity 。
- [MathJax Liquid Tags by Jessy Cowan-Sharp](https://gist.github.com/834610):用合适的 MathJax 标签替代相应的数学公式或方程式。
- [Non-JS Gist Tag by Brandon Tilley](https://gist.github.com/1027674): 嵌入 Gists ，显示给禁用 JavaScript 的用户。
- [Render Time Tag by Blake Smith](https://gist.github.com/449509): 显示页面的创建时间。
- [Status.net/OStatus Tag by phaer](https://gist.github.com/912466): 显示 status.net/ostatus 的通知。
- [Raw Tag by phaer](https://gist.github.com/1020852): 阻止转换 `raw` 标签的内容。
- [Embed.ly client by Robert Böhnke](https://github.com/robb/jekyll-embedly-client): Embed.ly 的实现。
- [Logarithmic Tag Cloud](https://gist.github.com/2290195): 支持对数。
- [oEmbed Tag by Tammo van Lessen](https://gist.github.com/1455726): 通过 oEmbed 支持内嵌第三方代码 (例如 YouTube, Flickr, Slideshare) 。
- [FlickrSetTag by Thomas Mango](https://github.com/tsmango/jekyll_flickr_set_tag): 将 Flickr 的图片生成画廊。
- [Tweet Tag by Scott W. Bradley](https://github.com/scottwb/jekyll-tweet-tag): [Tweets 支持](https://dev.twitter.com/docs/embedded-tweets) 。
- [Jekyll-contentblocks](https://github.com/rustygeldmacher/jekyll-contentblocks): 支持使用 Rails 风格的 content_for 标签。
- [Generate YouTube Embed](https://gist.github.com/1805814) by [joelverhagen](https://github.com/joelverhagen):支持以 YouTube ID 嵌入 YouTube 视频，宽高可配置。
- [Jekyll-beastiepress](https://github.com/okeeblow/jekyll-beastiepress): 可轻松连接到 FreeBSD 官网。
- [Jsonball](https://gist.github.com/1895282): 读取json文件并生成地图。
- [Bibjekyll](https://github.com/pablooliveira/bibjekyll): Render BibTeX-formatted bibliographies/citations included in posts and pages using bibtex2html.
- [Jekyll-citation](https://github.com/archome/jekyll-citation): 生成 BibTeX格式（ Holy shit! 还有多少要翻译）。
- [Jekyll Dribbble Set Tag](https://github.com/ericdfields/Jekyll-Dribbble-Set-Tag): 生成 Dribbble 画廊。
- [Debbugs](https://gist.github.com/2218470):可以轻松的链接到 Debian BTS 。
- [Refheap_tag](https://github.com/aburdette/refheap_tag): 支持[refheap](https://refheap.com).
- [Jekyll-devonly_tag](https://gist.github.com/2403522): 仅在开发环境使用的情况下可以考虑一下。
- [JekyllGalleryTag](https://github.com/redwallhp/JekyllGalleryTag) by [redwallhp](https://github.com/redwallhp): 生成缩略图，并展示。
- [Youku and Tudou Embed](https://gist.github.com/Yexiaoxing/5891929): 支持内嵌 Youku 和 Tudou 视频。
- [Jekyll-swfobject](https://github.com/sectore/jekyll-swfobject): 通过 [SWFObject](http://code.google.com/p/swfobject/) 支持内嵌 flash 。
- [Jekyll Picture Tag](https://github.com/robwierzbowski/jekyll-picture-tag): 相应式的图片，推荐 [`<picture>`](http://picture.responsiveimages.org/) ，改编自 Scott Jehl 的 [Picturefill](https://github.com/scottjehl/picturefill).
- [Jekyll Image Tag](https://github.com/robwierzbowski/jekyll-image-tag): 更好的图片处理插件，预先保存，生成调整大小后的图片，并且加好 `classes` 和 `alt` 等属性。
- [Ditaa Tag](https://github.com/matze/jekyll-ditaa) by [matze](https://github.com/matze): 将 ditta 格式的 ASCII 图片转换成 PNG。
- [Good Include](https://github.com/penibelst/jekyll-good-include) by [Anatol Broder](http://penibelst.de/): 去掉文件末尾的空行空格。
- [Jekyll Suggested Tweet](https://github.com/davidensinger/jekyll-suggested-tweet) by [David Ensinger](https://github.com/davidensinger/): 通过 Twitter 的 API 支持内嵌感兴趣的 tweets。

#### 集合

- [Jekyll Plugins by Recursive Design](http://recursive-design.com/projects/jekyll-plugins/): 生成 readme 说明文档，列表页以及网站地图。
- [Company website and blog plugins](https://github.com/flatterline/jekyll-plugins) by Flatterline, a [Ruby on Rails development company](http://flatterline.com/): Portfolio/project 的生成器, team/individual 的生成器，等等。
- [Jekyll plugins by Aucor](https://github.com/aucor/jekyll-plugins): 移除不需要的空格空行，并根据 weight 属性给页面排序。

#### 其他

- [Pygments Cache Path by Raimonds Simanovskis](https://github.com/rsim/blog.rayapps.com/blob/master/_plugins/pygments_cache_patch.rb): 缓存高亮代码核心模块。
- [Draft/Publish Plugin by Michael Ivey](https://gist.github.com/49630): 保存到草稿。
- [Growl Notification Generator by Tate Johnson](https://gist.github.com/490101): Jekyll 通知发送到 Growl 。
- [Growl Notification Hook by Tate Johnson](https://gist.github.com/525267): 同上，推荐指数更高一点，但是需要他的 “hook” 。
- [Related Posts by Lawrence Woodman](https://github.com/LawrenceWoodman/related_posts-jekyll_plugin): 重新实现关联，覆盖 `site.related_posts` 。
- [Tiered Archives by Eli Naeher](https://gist.github.com/88cda643aa7e3b0ca1e5): 创建 tiered 模板变量，允许按年月分组。
- [Jekyll-localization](https://github.com/blackwinter/jekyll-localization): 支持本地化。
- [Jekyll-rendering](https://github.com/blackwinter/jekyll-rendering): 一个渲染引擎。
- [Jekyll-pagination](https://github.com/blackwinter/jekyll-pagination): 支持分页。
- [Jekyll-tagging](https://github.com/pattex/jekyll-tagging): 生成云状标签。
- [Jekyll-scholar](https://github.com/inukshuk/jekyll-scholar): 为学者定制。
- [Jekyll-asset_bundler](https://github.com/moshen/jekyll-asset_bundler): 将 JavaScript 和 CSS 最小化。
- [Jekyll-assets](http://ixti.net/jekyll-assets/) by [ixti](https://github.com/ixti): Rails 风格的 assets pipeline（支持的资源 CoffeeScript, Sass, LESS 等等；设置依赖；最小化压缩；JST 模板；缓存处理等等）。
- [File compressor](https://gist.github.com/2758691) by [mytharcher](https://github.com/mytharcher): 压缩 HTML 和 JavaScript 。
- [Jekyll-minibundle](https://github.com/tkareine/jekyll-minibundle): 根据你选择的最小化工具绑定资源和处理缓存。
- [Singlepage-jekyll](https://github.com/JCB-K/singlepage-jekyll) by [JCB-K](https://github.com/JCB-K): 转换为单页网站。
- [generator-jekyllrb](https://github.com/robwierzbowski/generator-jekyllrb): [Yeoman](http://yeoman.io/) 的包装，一个工具集，还有工作流，用来创建现代化的网站。
- [grunt-jekyll](https://github.com/dannygarcia/grunt-jekyll)：[Grunt](http://gruntjs.com/) 插件。
- [jekyll-postfiles](https://github.com/indirect/jekyll-postfiles)：添加目录 `_postfiles`　和标签 {% raw %}`{{ postfile }}`{% endraw %}以保证所有的指向正确。

<div class="note info">
  <h5>期待你的作品</h5>
  <p>
    如果你有一个 Jekyll 插件并且愿意加到这个列表中来，可以<a href="../contributing/">阅读此须知</a>，并参照着来做。
  </p>
</div>
