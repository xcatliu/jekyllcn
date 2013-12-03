---
layout: docs
title: 博客迁移
prev_section: variables
next_section: templates
permalink: /docs/migrations/
contributor: debbbbie
---

如果你要从其他博客迁移到 Jekyll ， Jekyll 导入器可以帮助你。本页面的所有方法都需要旧系统数据库的
读权限，每个方法在 `_posts` 文件夹生成 `.markdown` 格式的文章。

## 迁移前的准备工作

导入器有很多的依赖，需要通过 gem [`jekyll-import`](https://github.com/jekyll/jekyll-import)
来完成。安装好本 gem 以后，就可以作为 Jekyll 的标准命令行来使用了。

{% highlight bash %}
$ gem install jekyll-import --pre
{% endhighlight %}

你应该已经准备好运行导入器了，如果碰到任何麻烦，可以看看导入器的帮助：

{% highlight bash %}
$ jekyll help import           # => See list of importers
$ jekyll help import IMPORTER  # => See importer specific help
{% endhighlight %}

其中的 IMPORTER 是某个导入器的名字。

<div class="note info">
  <h5>提示：记得复核迁移后的内容</h5>
  <p>

    导入器没有区分公开的和私有的文章，你要记得检查迁移后的文章是否你想要的。

  </p>
</div>

<!-- TODO all these need to be fixed -->

## WordPress

### WordPress 导出文件

如果还没有安装 hpricot ，你需要首先运行 `gem install hpricot` ；然后，用WordPress的导出
工具导出你的博客。假设导出的文件被保存为 `wordpress.xml` ，你需要运行如下命令：

{% highlight bash %}
$ ruby -rubygems -e 'require "jekyll/jekyll-import/wordpressdotcom";
    JekyllImport::WordpressDotCom.process({ :source => "wordpress.xml" })'
{% endhighlight %}

<div class="note">
  <h5>ProTip™: WordPress.com Export Tool</h5>
  <p markdown="1">If you are migrating from a WordPress.com account, you can
  access the export tool at the following URL:
  `https://YOUR-USER-NAME.wordpress.com/wp-admin/export.php`.</p>
</div>

### 使用 WordPress MySQL server 的连接

如果你想直接使用 WordPress MySQL server 的数据库连接，可以这样做：

{% highlight bash %}
$ ruby -rubygems -e 'require "jekyll/jekyll-import/wordpress";
    JekyllImport::WordPress.process({:dbname => "database", :user => "user", :pass => "pass"})'
{% endhighlight %}

如果你正在使用 Webfaction，并不得不建立一个
[SSH tunnel](http://docs.webfaction.com/user-guide/databases.html?highlight=mysql#starting-an-ssh-tunnel-with-ssh),
记得明确主机头(`127.0.0.1`) , 否则 MySQL 可能阻止连接，因为在认证系统中 `localhost` 和
`127.0.0.1` 是不同的：

{% highlight bash %}
$ ruby -rubygems -e 'require "jekyll/jekyll-import/wordpress";
    JekyllImport::WordPress.process({:host => "127.0.0.1", :dbname => "database", :user => "user", :pass => "pass"})'
{% endhighlight %}

### 功能更全的 WordPress 迁移工具

尽管上树方法可以工作，但他们并没有导入足够的元数据。如果你想导出诸如页面，标签，自定义字段，图片附件
等等，下边的资源或许对你有用：

- [Exitwp](https://github.com/thomasf/exitwp) is a configurable tool written in
  Python for migrating one or more WordPress blogs into Jekyll (Markdown) format
  while keeping as much metadata as possible. Exitwp also downloads attachments
  and pages.
- [A great
  article](http://vitobotta.com/how-to-migrate-from-wordpress-to-jekyll/) with a
  step-by-step guide for migrating a WordPress blog to Jekyll while keeping most
  of the structure and metadata.
- [wpXml2Jekyll](https://github.com/theaob/wpXml2Jekyll) is an executable
  windows application for creating Markdown posts from your WordPress XML file.

## Drupal

如果你是从 [Drupal](http://drupal.org) 导入，根据你的 Drupal 版本，有两个迁移工具供你使用：
- [Drupal 6](https://github.com/jekyll/jekyll-import/blob/v0.1.0.beta1/lib/jekyll/jekyll-import/drupal6.rb)
- [Drupal 7](https://github.com/jekyll/jekyll-import/blob/v0.1.0.beta1/lib/jekyll/jekyll-import/drupal7.rb)

{% highlight bash %}
$ ruby -rubygems -e 'require "jekyll/jekyll-import/drupal6";
    JekyllImport::Drupal6.process("dbname", "user", "pass")'
# ... or ...
$ ruby -rubygems -e 'require "jekyll/jekyll-import/drupal7";
    JekyllImport::Drupal7.process("dbname", "user", "pass")'
{% endhighlight %}

如果要连接到不同的主机或配置表前缀，你可以在迁移 Drupal 的执行代码后边加上下边两个参数：

{% highlight bash %}
$ ruby -rubygems -e 'require "jekyll/jekyll-import/drupal6";
    JekyllImport::Drupal6.process("dbname", "user", "pass", "host", "table_prefix")'
# ... or ...
$ ruby -rubygems -e 'require "jekyll/jekyll-import/drupal7";
    JekyllImport::Drupal7.process("dbname", "user", "pass", "host", "table_prefix")'
{% endhighlight %}

## Movable Type

从 Movable Type 导入：

{% highlight bash %}
$ ruby -rubygems -e 'require "jekyll/jekyll-import/mt";
    JekyllImport::MT.process("database", "user", "pass")'
{% endhighlight %}

## Typo

从 Typo 导入：

{% highlight bash %}
$ ruby -rubygems -e 'require "jekyll/jekyll-import/typo";
    JekyllImport::Typo.process("database", "user", "pass")'
{% endhighlight %}

这都代码仅仅在 Typo 版本 4 以上测试过。

## TextPattern

从 TextPattern 导入：

{% highlight bash %}
$ ruby -rubygems -e 'require "jekyll/jekyll-import/textpattern";
    JekyllImport::TextPattern.process("database_name", "username", "password", "hostname")'
{% endhighlight %}

你需要从 `_import` 所在文件夹的上级文件夹运行上述命令。例如， `_import` 的路径是
`/path/source/_import` ，你需要在 `/path/source` 运行上述命令。主机名默认为 `localhost` ，
其他变量需要这个参数。你或许要调整入口的代码。默认的，它将试图寻找所有可能的入口。

## Mephisto

从 Mephisto 导入：

{% highlight bash %}
$ ruby -rubygems -e 'require "jekyll/jekyll-import/mephisto";
    JekyllImport::Mephisto.process("database", "user", "password")'
{% endhighlight %}

如果你的数据放在 Postgres ，你需要用如下方法代替：

{% highlight bash %}
$ ruby -rubygems -e 'require "jekyll/jekyll-import/mephisto";
    JekyllImport::Mephisto.postgres({:database => "database", :username=>"username", :password =>"password"})'
{% endhighlight %}

## Blogger (Blogspot)

从 Blogger 导入，请参考文章[从 Blogger 迁移到 Jekyll](http://blog.coolaj86.com/articles/migrate-from-blogger-to-jekyll.html) 。
如果没有很好的工作，你可以试试下边的这些替代品：

- [@kennym](https://github.com/kennym) created a [little migration
  script](https://gist.github.com/1115810), because the solutions in the
  previous article didn't work out for him.
- [@ngauthier](https://github.com/ngauthier) created [another
  importer](https://gist.github.com/1506614) that imports comments, and does so
  via blogger’s archive instead of the RSS feed.
- [@juniorz](https://github.com/juniorz) created [yet another
  importer](https://gist.github.com/1564581) that works for
  [Octopress](http://octopress.org). It is like [@ngauthier’s
  version](https://gist.github.com/1506614) but separates drafts from posts, as
  well as importing tags and permalinks.

## Posterous

从 Posterous 导入：

{% highlight bash %}
$ ruby -rubygems -e 'require "jekyll/jekyll-import/posterous";
    JekyllImport::Posterous.process("my_email", "my_pass")'
{% endhighlight %}

如果要导出你帐号上的其他博客，需要配置 `blog_id` ：

{% highlight bash %}
$ ruby -rubygems -e 'require "jekyll/jekyll-import/posterous";
    JekyllImport::Posterous.process("my_email", "my_pass", "blog_id")'
{% endhighlight %}

有一个[替代品](https://github.com/pepijndevos/jekyll/blob/patch-1/lib/jekyll/migrators/posterous.rb)，
他保持了永久链接，并试图导入图片。

## Tumblr

从 Tumblr 导入：

{% highlight bash %}
$ ruby -rubygems -e 'require "jekyll/jekyll-import/tumblr";
    JekyllImport::Tumblr.process(url, format, grab_images, add_highlights, rewrite_urls)'
# url    - String: your blog's URL
# format - String: the output file extension. Use "md" to have your content
#          converted from HTML to Markdown. Defaults to "html".
# grab_images    - Boolean: whether to download images as well. Defaults to false.
# add_highlights - Boolean: whether to wrap code blocks (indented 4 spaces) in a Liquid
                   "highlight" tag. Defaults to false.
# rewrite_urls   - Boolean: whether to write pages that redirect from the old Tumblr paths
                   to the new Jekyll paths. Defaults to false.
{% endhighlight %}

## 其他

如果你有一个博客平台，而且还没有导入器，你可以考虑写一个，并提交给我们一个
 [ pull request](https://github.com/jekyll/jekyll-import).
