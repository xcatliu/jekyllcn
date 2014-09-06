---
layout: docs
title: 部署方法
prev_section: github-pages
next_section: troubleshooting
permalink: /docs/deployment-methods/
contributor: wenbing
---

Jekyll 生成的网站是静态的，因此有很多种部署方法。下面列出了一些常见的部署方法。

## 网站托管服务商 (FTP)

传统的网络托管服务商允许你使用 FTP 上传文件到他们的服务器。想通过 FTP 上传一个 Jekyll 站点，只需要运行 `jekyll` 命令然后复制生成的 `_site` 目录到你的托管账号根目录。多数托管服务商的跟目录会是 `httpdocs` 或 `public_html` 目录。

### 使用 Glynn 进行 FTP 上传

有一个叫 [Glynn](https://github.com/dmathieu/glynn) 的项目，可以帮助你简单的生成 Jekyll 站点并通过 FTP 发送到你的主机。

## 自己的网络服务器

如果你能够直接连接到部署的网络服务器，你可能有其它的方法传输文件 (如 `scp`，或者直接操作文件系统)，而其它过程都一样。要记住保证生成的 `_site` 目录放到网络服务器正确的根目录下。

## 自动化部署

也有一些自动化部署 Jekyll 站点的方法。下面列出了几种，如果你还有其它的，欢迎 [贡献](../contributing)，这样其它人就也能知道它了。

### Git post-update 钩子

如果你使用 [Git](http://git-scm.com) 管理你的 jekyll 站点，自动化部署非常简单，只需要给你的 Git 仓库设置一个 post-update 钩子，[就像这样](http://web.archive.org/web/20091223025644/http://www.taknado.com/en/2009/03/26/deploying-a-jekyll-generated-site/)

### Git post-receive 钩子

要让一个远程服务器在你每次用 Git 推送修改时进行部署，可以创建一个拥有所有要部署机器公钥的账号，然后设置 post-receive 钩子，其余的跟上面方法一样。

{% highlight bash %}
laptop$ ssh deployer@myserver.com
server$ mkdir myrepo.git
server$ cd myrepo.git
server$ git --bare init
server$ cp hooks/post-receive.sample hooks/post-receive
server$ mkdir /var/www/myrepo
{% endhighlight %}

接着, 添加下面的代码到 hooks/post-receive ，并保证服务器上已安装 Jekyll：

{% highlight bash %}
GIT_REPO=$HOME/myrepo.git
TMP_GIT_CLONE=$HOME/tmp/myrepo
PUBLIC_WWW=/var/www/myrepo

git clone $GIT_REPO $TMP_GIT_CLONE
jekyll build -s $TMP_GIT_CLONE -d $PUBLIC_WWW
rm -Rf $TMP_GIT_CLONE
exit
{% endhighlight %}

最后, 在任意可以通过此钩子部署的用户机器上运行下面的命令：

{% highlight bash %}
laptops$ git remote add deploy deployer@myserver.com:~/myrepo.git
{% endhighlight %}

剩下的就是告诉 nginx 或 Apache 监听 `/var/www/myrepo` 目录，然后运行下面的命令：

{% highlight bash %}
laptops$ git push deploy master
{% endhighlight %}

### Rake

另一个部署 Jekyll 站点的方法是使用 [Rake](https://github.com/jimweirich/rake)，[HighLine](https://github.com/JEG2/highline)，和 [Net::SSH](http://net-ssh.rubyforge.org/)。一个比较复杂的使用 Rake 部署多个分支的例子可以参考 [Git Ready](https://github.com/gitready/gitready/blob/en/Rakefile)。

### rsync

假如你已经生成了 `_site` 目录，就可以使用一个像 [部署脚本](http://github.com/henrik/henrik.nyh.se/blob/master/tasks/deploy) 这样的 shell 脚本 `tasks/deploy` rsync 到服务器了。当然需要修改你的站点相应的值。甚至还有 [一个 TextMate 匹配命令](http://gist.github.com/214959) 可以帮你在 Textmate 中运行这个脚本。
this script from within Textmate.

## Rack-Jekyll

[Rack-Jekyll](http://github.com/bry4n/rack-jekyll/) 是一个部署站点到任意 Rack 服务的简单方法，如 Amazon EC2, Slicehost, Heroku 等。它也可以 [shotgun](http://github.com/rtomakyo/shotgun/), [rackup](http://github.com/rack/rack), [mongrel](http://github.com/mongrel/mongrel), [unicorn](http://github.com/defunkt/unicorn/), and [others](https://github.com/adaoraul/rack-jekyll#readme) 一起运行。

可以阅读 [这篇文章](http://blog.crowdint.com/2010/08/02/instant-blog-using-jekyll-and-heroku.html) 了解如何使用 Rack-Jekyll 部署到 Heroku 。

## Jekyll-Admin for Rails

如果想在 Rails 中维护 Jekyll 站点，[Jekyll-Admin](http://github.com/zkarpinski/Jekyll-Admin) 包含了实现此功能直接可用的代码。详细可查看 Jekyll-Admin 的 [README](http://github.com/zkarpinski/Jekyll-Admin/blob/master/README) 。

## Amazon S3

如果要在 Amazon S3 上托管你的站点，可以使用 [s3_website](https://github.com/laurilehmijoki/s3_website) 。它会推送你的站点到 Amazon S3 上，Amazon S3 跟任意网络服务器一样，却能够动态扩容到几乎无限流量。这种方式适用小流量博客站点，因为你只需要为你使用的流量付费。

<div class="note">
  <h5>ProTip™: 使用 GitHub Pages 零麻烦托管</h5>
  <p>GitHub Pages 内部由 Jekyll 驱动, 所以如果你想找个零麻烦、零花费解决方案，Github Pages 是托管 <a href="../github-pages/">Jekyll 驱动站点</a>的首选。</p>
</div>
