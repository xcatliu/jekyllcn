---
layout: docs
title: Continuous Integration 持续集成
permalink: /docs/continuous-integration/
---

You can easily test your website build against one or more versions of Ruby.
对应于 Ruby 的一个或多个版本，你很容易就可以测试你的网站构建。
The following guide will show you how to set up a free build environment on
[Travis][0], with [GitHub][1] integration for pull requests. Paid
alternatives exist for private repositories.

以下指引将展示怎样在 [Travis][0] 上建立一个免费的，集成了处理 pull 请求的 [GitHub][1] 的构建环境。使用私有代码库的话，也有对应的付费选择。

[0]: https://travis-ci.org/
[1]: https://github.com/

## 1. Enabling Travis and GitHub
## 1. 启用 Travis 以及 Github

Enabling Travis builds for your GitHub repository is pretty simple:
启用 Travis 来构建你的 Github 代码库非常简单：

1. Go to your profile on travis-ci.org: https://travis-ci.org/profile/username
2. Find the repository for which you're interested in enabling builds.
3. Click the slider on the right so it says "ON" and is a dark grey.
4. Optionally configure the build by clicking on the wrench icon. Further
   configuration happens in your `.travis.yml` file. More details on that
   below.

1. 前往你在 travis-ci.org 的个人档案: https://travis-ci.org/profile/username
2. 选择需要启用构建的代码库。
3. 点击右侧的滑动按钮使其处于 "ON" 位置并成为深灰色。
4. 点击扳手图标可以进行一些配置，使用 `.travis.yaml` 文件可以进行更大范围的配置。更多详情可见于其下方。

## 2. The Test Script
## 2. 测试代码

The simplest test script simply runs `jekyll build` and ensures that Jekyll
doesn't fail to build the site. It doesn't check the resulting site, but it
does ensure things are built properly.

最简单的测试代码运行 `jekyll build` 来确保 Jekyll 对站点的构建不会出错。它并不检查站点的结果，而只确保构建正确地进行。

When testing Jekyll output, there is no better tool than [html-proofer][2].
This tool checks your resulting site to ensure all links and images exist.
Utilize it either with the convenient `htmlproof` command-line executable,
or write a Ruby script which utilizes the gem.

当需要测试 Jekyll 的输出结果时，[html-proofer][2] 是最佳的工具选择。这个工具会检查输出站点中所有的链接和图片的有效性。可以很方便地使用命令行 `htmlproof` 执行该工具，或者写一段 Ruby 代码来执行该 gem 。

### The HTML Proofer Executable
### HTML Proofer 命令行执行

{% highlight bash %}
#!/usr/bin/env bash
set -e # 出错时中止代码

bundle exec jekyll build
bundle exec htmlproof ./_site
{% endhighlight %}

Some options can be specified via command-line switches. Check out the
`html-proofer` README for more information about these switches, or run
`htmlproof --help` locally.

命令行执行时可通过参数切换一些选项。关于这些选项的信息请查看 `html-proofer` 的 README 文件，或者本地运行 `htmlproof --help` 。

### HTML Proofer 库

你也可以通过 Ruby 脚本来调用 `html-proofer`(例如在一个 Rakefile 中):

{% highlight ruby %}
#!/usr/bin/env ruby

require 'html/proofer'
HTML::Proofer.new("./_site").run
{% endhighlight %}

Options are given as a second argument to `.new`, and are encoded in a
symbol-keyed Ruby Hash. For more information about the configuration options,
check out `html-proofer`'s README file.

选项作为 `.new` 的第二参数传入，并编码为符号型键值的 Ruby 哈希 (symbol-keyed Ruby Hash)。要获得更多关于配置的选项，请参阅 `html-proofer` 的 README 文档。

[2]: https://github.com/gjtorikian/html-proofer

## 3. Configuring Your Travis Builds
## 3. 配置你的 Travis 构建

该文件用于配置你的 Travis 构建。由于 Jekyll 是基于 Ruby 的而且需要 RubyGems 来进行安装，我们使用 Ruby 语言环境。 范例的 `.travis.yml` 文件如下，后面会有每一行相应的解释。

**注意：** 你同时也需要一个 Gemfile, 基于相关的 gems, [Travis 将会自动安装](http://docs.travis-ci.com/user/languages/ruby/#Dependency-Management) 依赖组件：

{% highlight ruby %}
source "https://rubygems.org"

gem "jekyll"
gem "html-proofer"
{% endhighlight %}

{% highlight yaml %}
language: ruby
rvm:
- 2.1
# 假如 bundler 被使用，安装时将运行 `bundle install`.
script: ./script/cibuild

# 分支白名单
branches:
  only:
  - gh-pages     # 测试 gh-pages 分支
  - /pages-(.*)/ # 测试每一个以 "pages-" 开头的分支

env:
  global:
  - NOKOGIRI_USE_SYSTEM_LIBRARIES=true # 为 html-proofer 的安装加速
{% endhighlight %}

Ok, 接下来是每一行的解释：

{% highlight yaml %}
language: ruby
{% endhighlight %}

这一行告诉 Travis 应该使用一个 Ruby 构建容器。这将给予你 Bundler, RubyGems, 和一个 Ruby 运行库的脚本访问权。

{% highlight yaml %}
rvm:
- 2.1
{% endhighlight %}

RVM 是一个流行的 Ruby 版本管理器 (像 rbenv, chruby, 等等). 这一指令告诉 Travis 用来运行测试脚本的 Ruby 的版本。

{% highlight yaml %}
script: ./script/cibuild
{% endhighlight %}

Travis allows you to run any arbitrary shell script to test your site. One
convention is to put all scripts for your project in the `script`
directory, and to call your test script `cibuild`. This line is completely
customizable. If your script won't change much, you can write your test
incantation here directly:
Travis 允许用户运行任意自定义 shell 脚本来测试你的站点。惯用的一种方式是将项目的所有脚本放在 `script` 目录下，并将

{% highlight yaml %}
install: gem install jekyll html-proofer
script: jekyll build && htmlproof ./_site
{% endhighlight %}

The `script` directive can be absolutely any valid shell command.

{% highlight yaml %}
# branch whitelist
branches:
  only:
  - gh-pages     # test the gh-pages branch
  - /pages-(.*)/ # test every branch which starts with "pages-"
{% endhighlight %}

You want to ensure the Travis builds for your site are being run only on
the branch or branches which contain your site. One means of ensuring this
isolation is including a branch whitelist in your Travis configuration
file. By specifying the `gh-pages` branch, you will ensure the associated
test script (discussed above) is only executed on site branches. If you use
a pull request flow for proposing changes, you may wish to enforce a
convention for your builds such that all branches containing edits are
prefixed, exemplified above with the `/pages-(.*)/` regular expression.

The `branches` directive is completely optional.

{% highlight yaml %}
env:
  global:
  - NOKOGIRI_USE_SYSTEM_LIBRARIES=true # speeds up installation of html-proofer
{% endhighlight %}

Using `html-proofer`? You'll want this environment variable. Nokogiri, used
to parse HTML files in your compiled site, comes bundled with libraries
which it must compile each time it is installed. Luckily, you can
dramatically decrease the install time of Nokogiri by setting the
environment variable `NOKOGIRI_USE_SYSTEM_LIBRARIES` to `true`.

<div class="note warning">
  <h5>Be sure to exclude <code>vendor</code> from your
   <code>_config.yml</code></h5>
  <p>Travis bundles all gems in the <code>vendor</code> directory on its build
   servers, which Jekyll will mistakenly read and explode on.</p>
</div>

{% highlight yaml %}
exclude: [vendor]
{% endhighlight %}

### Questions?

This entire guide is open-source. Go ahead and [edit it][3] if you have a
fix or [ask for help][4] if you run into trouble and need some help.

[3]: https://github.com/jekyll/jekyll/edit/master/site/_docs/continuous-integration.md
[4]: https://github.com/jekyll/jekyll-help#how-do-i-ask-a-question
