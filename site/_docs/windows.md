---
layout: docs
title: Windows 运行Jekyll
permalink: /docs/windows/
translators: [comsince, StromKuo, xcatliu, baiyangcao, sctop] 
update_date: 2018-09-18
---

虽然 Windows 并不是 Jekyll 官方支持的平台，但是也可以通过合适的方法使其运行在 Windows 平台上。这个页面旨在收集一些由 Windows 用户发掘出来的关于 Jekyll 相关的知识和课程。

## 安装

JuLian Thilo 已经写出关于 [Jekyll 运行于Windows上][windows-installation] 的指南，并且看来适用于绝大数情况。这个说明是为 Ruby 2.0.0 写的，但是应该也适用了之后的版本 [2.2之前版本][hitimes-issue]

## 编码

如果你使用 UTF-8 编码，请确保你的文件头没有 `BOM` 字符，否则 Jekyll 将会出现意想不到的情况。尤其是当你想在 Windows 上使用 Jekyll 的时候。

另外，你可能需要将代码控制台页面的编码修改为 UTF-8，否则将会出现一个异常：在生成网页的时候，使用了不正确的编码。可以通过以下的命令解决：

{% highlight bash %}
$ chcp 65001
{% endhighlight %}

[windows-installation]: http://jekyll-windows.juthilo.com/
[hitimes-issue]: https://github.com/copiousfreetime/hitimes/issues/40

## 自动-重构建

到 1.3.0 后，当 `--watch` 开关在编译和运行是指定后，Jekyll 使用 gem 的 `listen` 去监听变化。然而 `listen` 只支持基于 UNIX 的操作系统，在 Windows 上需要一个额外的 gem 才能与其兼容。将下面的命令加入你的站点的 gemfile 中。

{% highlight ruby %}
gem 'wdm', '~> 0.1.0' if Gem.win_platform?
{% endhighlight %}


### 如何安装github-pages

本节是[Jens Willmer][jwillmerPost]所写的一篇文章的一部分，首先你需要在系统中安装[Chocolatey][]，如果你的系统中有其他版本的Ruby你需要先卸载。

#### 安装Ruby和Ruby development kit

打开命令行界面执行以下命令：

 * `choco install ruby -version 2.2.4`
 * `choco install ruby2.devkit` - _编译json gem时需要使用_

#### 配置Ruby development kit

Ruby开发工具包并没有设置Ruby环境变量，所以我们需要手动设置：

 * 在`C:\tools\DevKit2`目录下打开命令行界面
 * 执行`ruby dk.rb init`命令创建配置文件`config.yml`
 * 编辑文件`config.yml`在其中包含Ruby路径`- C:/tools/ruby22`
 * 执行命令创建路径： `ruby dk.rb install`

#### Nokogiri软件包安装

github-pages运行时需要Nokogiri这个软件包，但是要运行在64位Windows系统上还需要执行以下命令：


**注意:** 在当前版本 [pre release][nokogiriFails] 中提供了64位Windows系统支持，但是github-pages中并没有引用这个版本。


`choco install libxml2 -Source "https://www.nuget.org/api/v2/"`{:.language-ruby}

`choco install libxslt -Source "https://www.nuget.org/api/v2/"`{:.language-ruby}

`choco install libiconv -Source "https://www.nuget.org/api/v2/"`{:.language-ruby}

```ruby
 gem install nokogiri --^
   --with-xml2-include=C:\Chocolatey\lib\libxml2.2.7.8.7\build\native\include^
   --with-xml2-lib=C:\Chocolatey\lib\libxml2.redist.2.7.8.7\build\native\bin\v110\x64\Release\dynamic\cdecl^
   --with-iconv-include=C:\Chocolatey\lib\libiconv.1.14.0.11\build\native\include^
   --with-iconv-lib=C:\Chocolatey\lib\libiconv.redist.1.14.0.11\build\native\bin\v110\x64\Release\dynamic\cdecl^
   --with-xslt-include=C:\Chocolatey\lib\libxslt.1.1.28.0\build\native\include^
   --with-xslt-lib=C:\Chocolatey\lib\libxslt.redist.1.1.28.0\build\native\bin\v110\x64\Release\dynamic
```

#### 安装 github-pages

 * 打开命令行界面安装 [Bundler][]: `gem install bundler`
 * 在你的博客根目录中创建名为 `Gemfile` 不带任何后缀名的文件
 * 拷贝复制下面两行到文件中：


```ruby
source 'http://rubygems.org'
gem 'github-pages'
```

 * **注意:** 由于在使用的Ruby版本中使用SSL链接报错，所以这里我们使用不加密的链接
 * 打开命令行界面，切换到你本地博客库的根目录，安装github-pages: `bundle install`


这个过程完成之后你应该就已经在系统上安装了github-pages，此时你可以通过 `jekyll s` 命令来在本地启动你的博客。 \\
在启动的过程你会得到一个警告信息，提示你应该在 `Gemfile` 中包含 `gem 'wdm', '>= 0.1.0' if Gem.win_platform?`，
但是我在文件中添加了这一行之后 `jekyll s` 就不能正常启动了，所以我就直接无视了这个警告。

将来github-pages的安装应该像安装博客一样的简单，但是目前 Nokogiri ([v1.6.8][nokogiriReleases]) 的最新版并不是稳定版本，没有在github-pages中应用，故我们在Windows上还是要手动安装配置。

[jwillmerPost]: http://jwillmer.de/blog/tutorial/how-to-install-jekyll-and-pages-gem-on-windows-10-x46 "Installation instructions by Jens Willmer"
[Chocolatey]: https://chocolatey.org/install "Package manager for Windows"
[Bundler]: http://bundler.io/ "Ruby Dependencie Manager"
[nokogiriReleases]: https://github.com/sparklemotion/nokogiri/releases "Nokogiri Releases"
[nokogiriFails]: https://github.com/sparklemotion/nokogiri/issues/1456#issuecomment-206481794 "Nokogiri fails to install on Ruby 2.3 for Windows"

