---
layout: docs
title: 持续集成
permalink: /docs/continuous-integration/
translators: ikenbe
hash: 5647b91
---

对应于 Ruby 的一个或多个版本，你很轻松就可以测试你的网站构建。以下指引将展示怎样在 [Travis][0] 上建立一个免费的，集成了处理 pull 请求的 [GitHub][1] 的构建环境。如果你使用私有代码库的话，也有相应的付费选择。

[0]: https://travis-ci.org/
[1]: https://github.com/

## 1. 启用 Travis 以及 Github

启用 Travis 来构建你的 Github 代码库非常简单：

1. 前往你在 travis-ci.org 的个人档案: https://travis-ci.org/profile/username
2. 选择需要启用构建的代码库。
3. 点击右侧的滑动按钮使其处于 "ON" 位置并成为深灰色。
4. 点击扳手图标可以进行一些配置，使用 `.travis.yaml` 文件可以进行更大范围的配置。更多详情可见于其下方。

## 2. 测试代码

最简单的测试代码是运行 `jekyll build` 来确保 Jekyll 对站点的构建不会出错。它并不检查站点的输出结果，而只确保构建正确地进行。

当需要测试 Jekyll 的输出结果时，[html-proofer][2] 是最佳的工具选择。这个工具会检查输出站点中所有的链接和图片的有效性。可以很方便地使用命令行 `htmlproof` 执行该工具，或者写一段 Ruby 代码来执行该 gem 。

### HTML Proofer 命令行执行

{% highlight bash %}
#!/usr/bin/env bash
set -e # 出错时中止代码

bundle exec jekyll build
bundle exec htmlproof ./_site
{% endhighlight %}

命令行执行时可通过参数切换一些选项。关于这些选项的信息请查看 `html-proofer` 的 README 文件，或者本地运行 `htmlproof --help` 。

### HTML Proofer 库

你也可以通过 Ruby 脚本来调用 `html-proofer`(例如在一个 Rakefile 中):

{% highlight ruby %}
#!/usr/bin/env ruby

require 'html/proofer'
HTML::Proofer.new("./_site").run
{% endhighlight %}

选项作为 `.new` 的第二参数传入，并编码为符号型键值的 Ruby 哈希 (symbol-keyed Ruby Hash)。要获得更多关于配置的选项，请参阅 `html-proofer` 的 README 文档。

[2]: https://github.com/gjtorikian/html-proofer

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

Travis 允许用户运行任意自定义 shell 脚本来测试你的站点。惯用的一种方式是将项目的所有脚本放在 `script` 目录下，并将你的测试代码命名为 `cibuild`。当然这些都是可以完全自定义的。如果你的代码变化并不大，你也可以把你的测试语句这样写：

{% highlight yaml %}
install: gem install jekyll html-proofer
script: jekyll build && htmlproofer ./_site
{% endhighlight %}

此处的 `script` 指令可以是任何合法的 shell 命令。

{% highlight yaml %}
# 分支白名单
branches:
  only:
  - gh-pages     # 测试 gh-pages 分支
  - /pages-(.*)/ # 测试以 "pages-" 开头的所有分支
{% endhighlight %}

我们需要确保 Travis 为且只为包含了我们站点的分支进行构建，这可以通过在 Travis 的配置文件中加入一个分支白名单来实现。明确地加入 `gh-pages` 分支可以保证相关的 (上述) 测试脚本只在站点分支上运行。如果你使用 pull request flow 来提交修改，你可能希望添加一个构建规则，例如以上的正则表达式 `/pages-(.*)/`，让构建测试也涵盖了带有 pages 前缀的修改过的分支。

`branches` 指令是完全可选的。

{% highlight yaml %}
env:
  global:
  - NOKOGIRI_USE_SYSTEM_LIBRARIES=true # 加速 html-proofer 的安装
{% endhighlight %}

如果你在使用 `html-proofer`，建议使用这个环境变量。Nokogiri 在站点编译后被用来解析 HTML 文件，它每次安装都必须编译一遍所带的库文件。幸运的是，我们把环境变量 `NOKOGIRI_USE_SYSTEM_LIBRARIES` 设为 `true` 之后，将极大地降低 Nokogiri 所需的安装时间。

<div class="note warning">
  <h5>请确认将 <code>vendor</code> 从你的
   <code>_config.yml</code> 中排除 (exclude)</h5>
  <p>Travis 在它的构建服务器下的 <code>vendor</code> 目录中捆绑了所有的 gem, Jekyll 在此目录下会进行错误的读取并导致更严重的后果。</p>
</div>

{% highlight yaml %}
exclude: [vendor]
{% endhighlight %}

### 有疑问?

这篇指引完全是开源的。如果你想修复一个错误，可以前往 [编辑][3] 。假如你遇到了麻烦并需要一些帮助，请前往 [求助][4]

[3]: https://github.com/xcatliu/jekyllcn/edit/master/site/_docs/continuous-integration.md
[4]: https://talk.jekyllrb.com/
