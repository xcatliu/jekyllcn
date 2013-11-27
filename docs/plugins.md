---
layout: docs
title: 插件
prev_section: assets
next_section: extras
permalink: /docs/plugins/
contributor: debbbbie
---

Jekyll 支持插件功能，你可以很容易的加入自己的代码。

<div class="note info">
  <h5>在 GitHub Pages 使用插件</h5>
  <p>
    <a href="http://pages.github.com/">GitHub Pages</a>是由Jekyll提供技术支持的，考
    虑到安全因素，所有的 Pages 通过 <code>--safe</code> 选项禁用了插件功能，因此如果你的网
    站部署在 Github Pages ，那么你的插件不会工作。<br><br>
    不过仍然有办法发布到 GitHub Pages，你只需在本地做一些转换，并把生成好的文件上传到 Github
    替代 Jekyll 就可以了。
  </p>
</div>

## 安装插件

在网站根下目录建立 `_plugins` 文件夹，插件放在这里即可。 Jekyll 运行之前，会加载此目录下所有以
 `*.rb` 结尾的文件。

通常，插件最终会被放在以下的目录中：

1. Generators
2. Converters
3. Tags

## 生成

你可以像下边这样编写一个生成器：

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

本例中，生成器在 `categories` 下生成了一系列文件。并使用布局 `category_index.html` 列出所有
的文章。

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

## 转换器

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
        检查文件后缀名是否是所要的，传入的参数是文件的后缀名（包括点号），接受的返回值是
         <code>true</code> 或 <code>false</code> 。
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

在上边的例子中， `UpcaseConverter#matches` 检查文件后缀名是不是 `.upcase` ;
`UpcaseConverter#convert` 会处理检查成功文件的内容，即将所有的字符串变成大写；最终，保存的结果
将以作为后缀名 `.html` 。

## 标记

如果你想使用 liquid 标记，你可以这样做。 Jekyll 官方的例子有 `highlight` 和 `include` 等
标记。下边的例子中，自定义了一个 liquid 标记，用来输出当前时间：

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

你必须同时用Liquid模板引擎注册自定义标记，比如：：

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

你可以像上边那样在 Liquid 模板中加入自己的过滤器。过滤器会把自己的方法暴露给 liquid 。所有的方法
都必须至少接收一个参数，用来传输入内容；返回值是过滤的结果。

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
    Jekyll 允许通过 Liquid 的<code>context.registers</code> 特性来访问
    <code>site</code> 对象。比如可以用 <code>context.registers.config</code>
    访问配置文件 <code>_config.yml</code> 。
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
          告诉 Jekyll 此插件是否可以安全的执行任意代码。 GitHub Pages 用他来决定那个插件可以
          使用，哪些不可以使用。如果你的插件不允许执行任意代码，把它设为 <code>true</code> 即
          可。 GitHub Pages 仍然不会加载你的插件，但是如果你把他夹杂到核心中，最后保证此值设置
          的正确！
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>priority</code></p>
      </td>
      <td>
        <p>
          此标记决定加载插件的顺序。可以是这些值： <code>:lowest</code>, <code>:low</code>,
           <code>:normal</code> ， <code>:high</code> ，还有 <code>:highest</code>。
          优先级高的先执行，优先级低的后执行。
        </p>
      </td>
    </tr>
  </tbody>
</table>
</div>

已上边例子的插件为例，应该这样设置这两个标记：

{% highlight ruby %}
module Jekyll
  class UpcaseConverter < Converter
    safe true
    priority :low
    ...
  end
end
{% endhighlight %}

## 可用的插件

下边的插件，你可以按需所取：

#### 生成器

- [ArchiveGenerator by Ilkka Laukkanen](https://gist.github.com/707909)：用[这里的方法](https://gist.github.com/707020)生成档案。
- [LESS.js Generator by Andy Fowler](https://gist.github.com/642739)：生成的时候产生 LESS.js 文件。
- [Version Reporter by Blake Smith](https://gist.github.com/449491)：创建包含 Jekyll 版本的文件 version.html 。
- [Sitemap.xml Generator by Michael Levin](https://github.com/kinnetica/jekyll-plugins)：遍历所有的页面和文章，生成 sitemap.xml 。
- [Full-text search by Pascal Widdershoven](https://github.com/PascalW/jekyll_indextank)：全文搜索。
- [AliasGenerator by Thomas Mango](https://github.com/tsmango/jekyll_alias_generator)：根据YAML头信息中的 alias　生成跳转页面。
- [Pageless Redirect Generator by Nick Quinlan](https://github.com/nquinlan/jekyll-pageless-redirects)：根据Jekyll跟路径做出跳转，支持分布式。
- [Projectlist by Frederic Hemberger](https://github.com/fhemberger/jekyll-projectlist): Renders files in a directory as a single page instead of separate posts.
- [RssGenerator by Assaf Gelber](https://github.com/agelber/jekyll-rss): Automatically creates an RSS 2.0 feed from your posts.

#### 转换器

- [Jade plugin by John Papandriopoulos](https://github.com/snappylabs/jade-jekyll-plugin): Jade converter for Jekyll.
- [HAML plugin by Sam Z](https://gist.github.com/517556): HAML converter for Jekyll.
- [HAML-Sass Converter by Adam Pearson](https://gist.github.com/481456): Simple HAML-Sass converter for Jekyll. [Fork](https://gist.github.com/528642) by Sam X.
- [Sass SCSS Converter by Mark Wolfe](https://gist.github.com/960150): Sass converter which uses the new CSS compatible syntax, based Sam X’s fork above.
- [LESS Converter by Jason Graham](https://gist.github.com/639920): Convert LESS files to CSS.
- [LESS Converter by Josh Brown](https://gist.github.com/760265): Simple LESS converter.
- [Upcase Converter by Blake Smith](https://gist.github.com/449463): An example Jekyll converter.
- [CoffeeScript Converter by phaer](https://gist.github.com/959938): A [CoffeeScript](http://coffeescript.org) to Javascript converter.
- [Markdown References by Olov Lassus](https://github.com/olov/jekyll-references): Keep all your markdown reference-style link definitions in one \_references.md file.
- [Stylus Converter](https://gist.github.com/988201): Convert .styl to .css.
- [ReStructuredText Converter](https://github.com/xdissent/jekyll-rst): Converts ReST documents to HTML with Pygments syntax highlighting.
- [Jekyll-pandoc-plugin](https://github.com/dsanson/jekyll-pandoc-plugin): Use pandoc for rendering markdown.
- [Jekyll-pandoc-multiple-formats](https://github.com/fauno/jekyll-pandoc-multiple-formats) by [edsl](https://github.com/edsl): Use pandoc to generate your site in multiple formats. Supports pandoc’s markdown extensions.
- [ReStructuredText Converter](https://github.com/xdissent/jekyll-rst): Converts ReST documents to HTML with Pygments syntax highlighting.
- [Transform Layouts](https://gist.github.com/1472645): Allows HAML layouts (you need a HAML Converter plugin for this to work).

#### 过滤器

- [Truncate HTML](https://github.com/MattHall/truncatehtml) by [Matt Hall](http://codebeef.com): A Jekyll filter that truncates HTML while preserving markup structure.
- [Domain Name Filter by Lawrence Woodman](https://github.com/LawrenceWoodman/domain_name-liquid_filter): Filters the input text so that just the domain name is left.
- [Summarize Filter by Mathieu Arnold](https://gist.github.com/731597): Remove markup after a `<div id="extended">` tag.
- [URL encoding by James An](https://gist.github.com/919275): Percent encoding for URIs.
- [JSON Filter](https://gist.github.com/1850654) by [joelverhagen](https://github.com/joelverhagen): Filter that takes input text and outputs it as JSON. Great for rendering JavaScript.
- [i18n_filter](https://github.com/gacha/gacha.id.lv/blob/master/_plugins/i18n_filter.rb): Liquid filter to use I18n localization.
- [Smilify](https://github.com/SaswatPadhi/jekyll_smilify) by [SaswatPadhi](https://github.com/SaswatPadhi): Convert text emoticons in your content to themeable smiley pics ([Demo](http://saswatpadhi.github.com/)).
- [Read in X Minutes](https://gist.github.com/zachleat/5792681) by [zachleat](https://github.com/zachleat): Estimates the reading time of a string (for blog post content).
- [Jekyll-timeago](https://github.com/markets/jekyll-timeago): Converts a time value to the time ago in words.
- [pluralize](https://github.com/bdesham/pluralize): Easily combine a number and a word into a gramatically-correct amount like “1 minute” or “2 minute**s**”.
- [reading_time](https://github.com/bdesham/reading_time): Count words and estimate reading time for a piece of text, ignoring HTML elements that are unlikely to contain running text.
- [Table of Content Generator](https://github.com/dafi/jekyll-toc-generator): Generate the HTML code containing a table of content (TOC), the TOC can be customized in many way, for example you can decide which pages can be without TOC.

#### 标签

- [Delicious Plugin by Christian Hellsten](https://github.com/christianhellsten/jekyll-plugins): Fetches and renders bookmarks from delicious.com.
- [Ultraviolet Plugin by Steve Alex](https://gist.github.com/480380): Jekyll tag for the [Ultraviolet](http://ultraviolet.rubyforge.org/) code highligher.
- [Tag Cloud Plugin by Ilkka Laukkanen](https://gist.github.com/710577): Generate a tag cloud that links to tag pages.
- [GIT Tag by Alexandre Girard](https://gist.github.com/730347): Add Git activity inside a list.
- [MathJax Liquid Tags by Jessy Cowan-Sharp](https://gist.github.com/834610): Simple liquid tags for Jekyll that convert inline math and block equations to the appropriate MathJax script tags.
- [Non-JS Gist Tag by Brandon Tilley](https://gist.github.com/1027674) A Liquid tag that embeds Gists and shows code for non-JavaScript enabled browsers and readers.
- [Render Time Tag by Blake Smith](https://gist.github.com/449509): Displays the time a Jekyll page was generated.
- [Status.net/OStatus Tag by phaer](https://gist.github.com/912466): Displays the notices in a given status.net/ostatus feed.
- [Raw Tag by phaer](https://gist.github.com/1020852): Keeps liquid from parsing text betweeen `raw` tags.
- [Embed.ly client by Robert Böhnke](https://github.com/robb/jekyll-embedly-client): Autogenerate embeds from URLs using oEmbed.
- [Logarithmic Tag Cloud](https://gist.github.com/2290195): Flexible. Logarithmic distribution. Documentation inline.
- [oEmbed Tag by Tammo van Lessen](https://gist.github.com/1455726): Enables easy content embedding (e.g. from YouTube, Flickr, Slideshare) via oEmbed.
- [FlickrSetTag by Thomas Mango](https://github.com/tsmango/jekyll_flickr_set_tag): Generates image galleries from Flickr sets.
- [Tweet Tag by Scott W. Bradley](https://github.com/scottwb/jekyll-tweet-tag): Liquid tag for [Embedded Tweets](https://dev.twitter.com/docs/embedded-tweets) using Twitter’s shortcodes.
- [Jekyll-contentblocks](https://github.com/rustygeldmacher/jekyll-contentblocks): Lets you use Rails-like content_for tags in your templates, for passing content from your posts up to your layouts.
- [Generate YouTube Embed](https://gist.github.com/1805814) by [joelverhagen](https://github.com/joelverhagen): Jekyll plugin which allows you to embed a YouTube video in your page with the YouTube ID. Optionally specify width and height dimensions. Like “oEmbed Tag” but just for YouTube.
- [Jekyll-beastiepress](https://github.com/okeeblow/jekyll-beastiepress): FreeBSD utility tags for Jekyll sites.
- [Jsonball](https://gist.github.com/1895282): Reads json files and produces maps for use in Jekyll files.
- [Bibjekyll](https://github.com/pablooliveira/bibjekyll): Render BibTeX-formatted bibliographies/citations included in posts and pages using bibtex2html.
- [Jekyll-citation](https://github.com/archome/jekyll-citation): Render BibTeX-formatted bibliographies/citations included in posts and pages (pure Ruby).
- [Jekyll Dribbble Set Tag](https://github.com/ericdfields/Jekyll-Dribbble-Set-Tag): Builds Dribbble image galleries from any user.
- [Debbugs](https://gist.github.com/2218470): Allows posting links to Debian BTS easily.
- [Refheap_tag](https://github.com/aburdette/refheap_tag): Liquid tag that allows embedding pastes from [refheap](https://refheap.com).
- [Jekyll-devonly_tag](https://gist.github.com/2403522): A block tag for including markup only during development.
- [JekyllGalleryTag](https://github.com/redwallhp/JekyllGalleryTag) by [redwallhp](https://github.com/redwallhp): Generates thumbnails from a directory of images and displays them in a grid.
- [Youku and Tudou Embed](https://gist.github.com/Yexiaoxing/5891929): Liquid plugin for embedding Youku and Tudou videos.
- [Jekyll-swfobject](https://github.com/sectore/jekyll-swfobject): Liquid plugin for embedding Adobe Flash files (.swf) using [SWFObject](http://code.google.com/p/swfobject/).
- [Jekyll Picture Tag](https://github.com/robwierzbowski/jekyll-picture-tag): Easy responsive images for Jekyll. Based on the proposed [`<picture>`](http://picture.responsiveimages.org/) element, polyfilled with Scott Jehl’s [Picturefill](https://github.com/scottjehl/picturefill).
- [Jekyll Image Tag](https://github.com/robwierzbowski/jekyll-image-tag): Better images for Jekyll. Save image presets, generate resized images, and add classes, alt text, and other attributes.
- [Ditaa Tag](https://github.com/matze/jekyll-ditaa) by [matze](https://github.com/matze): Renders ASCII diagram art into PNG images and inserts a figure tag.
- [Good Include](https://github.com/penibelst/jekyll-good-include) by [Anatol Broder](http://penibelst.de/): Strips newlines and whitespaces from the end of include files before processing.
- [Jekyll Suggested Tweet](https://github.com/davidensinger/jekyll-suggested-tweet) by [David Ensinger](https://github.com/davidensinger/): A Liquid tag for Jekyll that allows for the embedding of suggested tweets via Twitter’s Web Intents API.

#### 集合

- [Jekyll Plugins by Recursive Design](http://recursive-design.com/projects/jekyll-plugins/): Plugins to generate Project pages from GitHub readmes, a Category page, and a Sitemap generator.
- [Company website and blog plugins](https://github.com/flatterline/jekyll-plugins) by Flatterline, a [Ruby on Rails development company](http://flatterline.com/): Portfolio/project page generator, team/individual page generator, an author bio liquid tag for use on posts, and a few other smaller plugins.
- [Jekyll plugins by Aucor](https://github.com/aucor/jekyll-plugins): Plugins for trimming unwanted newlines/whitespace and sorting pages by weight attribute.

#### 其他

- [Pygments Cache Path by Raimonds Simanovskis](https://github.com/rsim/blog.rayapps.com/blob/master/_plugins/pygments_cache_patch.rb): Plugin to cache syntax-highlighted code from Pygments.
- [Draft/Publish Plugin by Michael Ivey](https://gist.github.com/49630): Save posts as drafts.
- [Growl Notification Generator by Tate Johnson](https://gist.github.com/490101): Send Jekyll notifications to Growl.
- [Growl Notification Hook by Tate Johnson](https://gist.github.com/525267): Better alternative to the above, but requires his “hook” fork.
- [Related Posts by Lawrence Woodman](https://github.com/LawrenceWoodman/related_posts-jekyll_plugin): Overrides `site.related_posts` to use categories to assess relationship.
- [Tiered Archives by Eli Naeher](https://gist.github.com/88cda643aa7e3b0ca1e5): Create tiered template variable that allows you to group archives by year and month.
- [Jekyll-localization](https://github.com/blackwinter/jekyll-localization): Jekyll plugin that adds localization features to the rendering engine.
- [Jekyll-rendering](https://github.com/blackwinter/jekyll-rendering): Jekyll plugin to provide alternative rendering engines.
- [Jekyll-pagination](https://github.com/blackwinter/jekyll-pagination): Jekyll plugin to extend the pagination generator.
- [Jekyll-tagging](https://github.com/pattex/jekyll-tagging): Jekyll plugin to automatically generate a tag cloud and tag pages.
- [Jekyll-scholar](https://github.com/inukshuk/jekyll-scholar): Jekyll extensions for the blogging scholar.
- [Jekyll-asset_bundler](https://github.com/moshen/jekyll-asset_bundler): Bundles and minifies JavaScript and CSS.
- [Jekyll-assets](http://ixti.net/jekyll-assets/) by [ixti](https://github.com/ixti): Rails-alike assets pipeline (write assets in CoffeeScript, Sass, LESS etc; specify dependencies for automatic bundling using simple declarative comments in assets; minify and compress; use JST templates; cache bust; and many-many more).
- [File compressor](https://gist.github.com/2758691) by [mytharcher](https://github.com/mytharcher): Compress HTML and JavaScript files on site build.
- [Jekyll-minibundle](https://github.com/tkareine/jekyll-minibundle): Asset bundling and cache busting using external minification tool of your choice. No gem dependencies.
- [Singlepage-jekyll](https://github.com/JCB-K/singlepage-jekyll) by [JCB-K](https://github.com/JCB-K): Turns Jekyll into a dynamic one-page website.
- [generator-jekyllrb](https://github.com/robwierzbowski/generator-jekyllrb): A generator that wraps Jekyll in [Yeoman](http://yeoman.io/), a tool collection and workflow for builing modern web apps.
- [grunt-jekyll](https://github.com/dannygarcia/grunt-jekyll)： [Grunt](http://gruntjs.com/)　插件。
- [jekyll-postfiles](https://github.com/indirect/jekyll-postfiles)：　添加目录 `_postfiles`　和标签 {% raw %}`{{ postfile }}`{% endraw %}以保证所有的指向正确。

<div class="note info">
  <h5>Jekyll Plugins Wanted</h5>
  <p>
    If you have a Jekyll plugin that you would like to see added to this list,
    you should <a href="../contributing/">read the contributing page</a> to find
    out how to make that happen.
  </p>
</div>
