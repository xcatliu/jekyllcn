---
layout: docs
title: 主题
permalink: /docs/themes/
translators: [AlanTanis, baiyangcao]
update_date: 2016-10-21
---

Jekyll 包含有一个强大的主题系统，因此您可以使用社区的模板和样式来定制自己的站点。Jekyll 主题打包了布局文件、包含文件及样式表。同时您也可以使用自己站点的内容去覆盖它们的默认内容。

## 安装主题

1. 若要安装一套主题，请先将该主题添加到您站点的 `Gemfile` 中：

        gem 'my-awesome-jekyll-theme'

2. 保存并应用 `Gemfile` 中相关的文件变化。
3. 执行命令行 `bundle install` 来安装主题。
4. 最后, 向您站点的 `_config.yml` 中加入下列代码来启用主题：

        theme: my-awesome-jekyll-theme

您可以在站点的 Gemfile 中留有多套主题，但在 `_config.yml` 中您只能选择一套来激活使用。
{: .note .info }

## 覆盖主题默认内容

Jekyll 主题含有主题默认的布局文件、包含文件和样式表，但您可以使用自己站点的内容去覆盖它们。举个例子，如果您选择使用一个具有 `page` 布局的主题，您能通过在 `_layouts` 文件夹下创建一个属于自己的 `page` 布局文件(例如 `_layouts/page.html`)来覆盖当前主题的布局。

在下列文件夹中，Jekyll 会优先查看您站点中的内容，然后查看主题的默认内容：

* `/assets`
* `/_layouts`
* `/_includes`
* `/_sass`

关于允许用户覆盖的主题内容，请参考您所选主题的文档和源仓库来获取更多信息。
{: .note .info}

如果想要定位电脑上主题文件的位置，执行命令 `bundle show` 加上主题包的名称，
如： `bundle show minima` 命令来查询 Jekyll 默认主题包的位置，
然后从返回的路径拷贝你想要重写的文件到你的网站根目录中。

## 创建一套主题

Jekyll 的主题通过 Ruby gems 进行分发。同时 [Ruby Gemspec](http://guides.rubygems.org/specification-reference/) 是唯一必需的文件。这里有个 `my-awesome-jekyll-theme` 主题简短的小例子，它保存在 `/my-awsome-jekyll-theme.gemspec` 下:

{% highlight ruby %}
Gem::Specification.new do |s|
  s.name     = '<THEME TITLE>'
  s.version  = '0.1.0'
  s.license  = 'MIT'
  s.summary  = '<THEME DESCRIPTION>'
  s.author   = '<YOUR NAME>'
  s.email    = '<YOUR EMAIL>'
  s.homepage = 'https://github.com/jekyll/my-awesome-jekyll-theme'
  s.files    = `git ls-files -z`.split("\x0").grep(%r{^_(sass|includes|layouts)/})
end
{% endhighlight %}

### 布局（Layouts）和包含文件（includes）

主题的布局文件和包含文件起到的作用，与它们在 Jekyll 站点中时无异。请将布局文件放置在 `/_layouts` 文件夹中，同时将包含文件放置在您主题的 `/_includes` 文件夹中。

举个例子，假设您的主题拥有一个 `/_layouts/page.html` 文件，和一个带有 `layout: page` 头信息的页面。Jekyll 将优先检查站点中 `_layouts` 文件夹下关于 `page` 的布局。如果没有，那就会使用您主题中关于 `page` 的布局。

### 样式表

您主题的样式表应当放置在您主题的 `/_sass` 文件夹中。就像在制作您的 Jekyll 站点时那样。通过使用 `@import` 指令，用户能将您主题中的样式包含到他的样式表中。

### 为主题撰写文档

您的主题应当包含有一份 `/README.md` 文件，其说明了类似这些内容，比如，用户该如何安装并使用您的主题？里面有怎样的布局文件？有哪些包含文件？以及是否要对站点的配置文件做额外的修改？

### 附上一个截图

主题是一种视觉形象化的表达。为了向用户展示您主题的样式，您可以在主题的仓库（repository）中包含一个 `/screenshot.png` 的截图。因为在那儿您可以便捷地修改相关内容。同时，您也可以在主题的文档中附上主题的相关截图。

### 预览您的主题

在您制作主题的过程中，若想要预览它，那么向其加入一些假内容（dummy content）或许会对您有所帮助，比如 `/index.html` 和 `/page.html` 文件。这将允许您使用 `jekyll build` 和 `jekyll serve` 命令来预览您的主题，就像预览一个 Jekyll 站点那样。

如果在本地预览您的主题，请确保已将 `/_site` 添加到您主题的 `.gitignore` 文件中。这会让您避免在分发主题的过程中，把自己已生成的站点也包含进去。
{: .info .note}

### 发布您的主题

主题均通过 [RubyGems.org](https://rubygems.org) 进行发布。在这过程中会要求您拥有一个 RubyGems 账户。当然，您可以 [免费创建](https://rubygems.org/sign_up) 一个账户。

1. 首先，执行以下的命令行来打包您的主题。记得把 `my-awesome-jekyll-theme` 替换成您主题的名字：

        gem build my-awesome-jekyll-theme.gemspec

2. 然后，执行以下的命令行来将您的主题包推送到 RubyGems 服务上。同样记得把 `my-awesome-jekyll-theme` 替换成您主题的名字：

        gem push my-awesome-jekyll-theme-*.gem
