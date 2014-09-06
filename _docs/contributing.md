---
layout: docs
title: 贡献
prev_section: upgrading
next_section: history
permalink: /docs/contributing/
contributor: debbbbie
---

是不是有个点子想实现到 Jekyll 。太好了，请参照如下： Great! Please keep the
following in mind:

* 如果你要在已有的特性上做一个小修补，只需要写一个简单的 test 就可以了。在当前测试中使用
  [Shoulda](http://github.com/thoughtbot/shoulda/tree/master) 和
  [RR](http://github.com/btakita/rr/tree/master).
* 如果是一个新特性，请写一个新的 [Cucumber](https://github.com/cucumber/cucumber/) 并在
  适当的地方重用步骤。同样，你也可以大胆的修改你对本网站的拷贝，一旦被合并掉，就会展示到网站 jekyllrb.com 。
* 如果你改变了 Jekyll 的习惯，不要忘了及时更新文档。在 `site/docs` 里边。如果发现文档中缺失的信息，
  赶快加上吧。伟大的文档造就伟大的项目！
* 当修改 Ruby 代码的时候，请遵照 [GitHub Ruby 编码规范](https://github.com/styleguide/ruby)。
* 请尽可能的提交 **小的 pull request** 。修改内容看起来越简单，就越可能被合并到主分支。
* 当提交 pull request 时，要知道什么地方放什么东西。描述一下做了哪些修改，背后的动机以及
  [完成了什么任务或有待完成的](http://git.io/gfm-tasks)都会加快复核。

<div class="note warning">
  <h5>不接受没有测试的代码</h5>
  <p>
    如果你要在已有的特性上做一个小修补，只需要写一个简单的 test 就可以了。
  </p>
</div>

测试依赖
-----------------

想要跑测试用例和编译 gem 的话，你需要安装 Jekyll 的依赖包。Jekyll 支持 Bundler ，所以只需要运
行一下 `bundle` 就可以了。

{% highlight bash %}
$ bundle
{% endhighlight %}

 在开始之前，跑一下测试代码以确信全部通过（确定一下你的环境配置好了）：

{% highlight bash %}
$ bundle exec rake test
$ bundle exec rake features
{% endhighlight %}

Workflow
--------

这是最直接的途径： the most direct way to get your work merged into the project:

* Fork 本项目。
* 从你的fork下载到本地：

{% highlight bash %}
git clone git://github.com/<username>/jekyll.git
{% endhighlight %}

* 创建一个分支，包含要修改的内容：

{% highlight bash %}
git checkout -b my_awesome_feature
{% endhighlight %}


* 添加测试。
* 通过命令 `rake` 确定所有测试依然全部通过。
* 如果有必要，将你的提交合并到逻辑块里边，不能有错误。
* 可以推送本分支了：

{% highlight bash %}
git push origin my_awesome_feature
{% endhighlight %}

* 同 mojombo/jekyll:master 对比并创建一个 pull request ，描述一下你改了什么还有你为什么认为
  他们会合并你的代码。

更新文档
----------------------

我们希望 Jekyll的文档尽可能的优秀。我们已经开源了所有文档，欢迎提交修改。

你可以在[这里]({{ site.repository }}/tree/master/site)找到 jekyllrb.com 的文档。

所有针对文档的 pull requests 都要放在 `master` 。不允许提交到其他分支。

Github 上的 [Jekyll wiki]({{ site.repository }}/wiki)可以自由更新，不需要 pull request，
任何人都可以修改。

陷阱
-------

* 如果你想修改 gem 版本，请放在一个独立的提交里边。如此，维护人员方便管理一些。 
* 尽量让你分支中的代码是最新的。
* 不要在你的 GitHub issue 用 [fix], [feature] 等标记。维护人员会积极的阅读 issues，一 旦碰到他们会主动标记。



<div class="note">
  <h5>帮助我们做的更好</h5>
  <p>
    Both不管使用还是为 Jekyll 贡献代码，都应该是有趣的、简单的、轻松的，所以如果你发现有什么不适，
    请在 Github 上 <a href="{{ site.repository }}/issues/new">提交一个 issue</a> 。
  </p>
</div>
