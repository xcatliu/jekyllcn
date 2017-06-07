---
layout: docs
title: 部署方法
permalink: /docs/deployment-methods/
translators: wenbing
---

Jekyll 生成的网站是静态的，因此有很多种部署方法。下面列出了一些常见的部署方法。

## 网站托管服务商 (FTP)

传统的网络托管服务商允许你使用 FTP 上传文件到他们的服务器。想通过 FTP 上传一个 Jekyll 站点，只需要运行 `jekyll` 命令然后复制生成的 `_site` 目录到你的托管账号根目录。多数托管服务商的根目录会是 `httpdocs` 或 `public_html` 目录。

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

### Static Publisher

[Static Publisher](https://github.com/static-publisher/static-publisher) 是另一种使用监听网络钩子提交服务器的自动化部署方式，
虽然并没有特别与Github绑定。提供一键部署到 Heroku 功能，可以监控一个服务器上的各种项目，
还提供了简便的用户管理接口，并且可以发布到 S3 或者 Git 仓库（如： gh-pages ）。

### Rake

另一个部署 Jekyll 站点的方法是使用 [Rake](https://github.com/jimweirich/rake)，[HighLine](https://github.com/JEG2/highline)，和 [Net::SSH](http://net-ssh.rubyforge.org/)。一个比较复杂的使用 Rake 部署多个分支的例子可以参考 [Git Ready](https://github.com/gitready/gitready/blob/en/Rakefile)。

### scp

一旦生成了 `_site` 目录，你可以使用一个 `tasks/deploy` shell脚本来部署网站，
如：这个[部署脚本](https://github.com/henrik/henrik.nyh.se/blob/master/script/deploy)。
当然你需要根据你的网站信息修改脚本的相关配置值。这些一般的[TextMate匹配命令](https://gist.github.com/henrik/214959)可以帮助你执行这个脚本。

### rsync

假如你已经生成了 `_site` 目录，就可以使用一个像 [部署脚本](https://github.com/vitalyrepin/vrepinblog/blob/master/transfer.sh) 这样的 shell 脚本 `tasks/deploy` rsync 到服务器了。当然需要修改你的站点相应的值。

基于证书的验证是简化发布流程的另一种方式，限制 rsync 仅能访问你想要同步的目录也更合理，
这可以使用 rrsync 来实现。

#### 第一步：在 home 目录安装 rrsync （服务端）

如果你的主机上没有安装 rrsync ，你可以自行安装：

 - [下载 rrsync](https://ftp.samba.org/pub/unpacked/rsync/support/rrsync)
 - 放在你的 home 目录的 `bin` 子目录里 （`~/bin`）
 - 使之可执行（ `chmod +x` ）

#### 第二步：设置基于证书的 SSH 访问权限（服务端）

这个[流程](https://wiki.gentoo.org/wiki/SSH#Passwordless_Authentication)网上随处可见，
与典型方法不同的是需要在 `~/.ssh/authorized_keys` 文件中加入基于证书验证的限制。
然后，启动 `rrsync` 并提供其应该具有读写权限的目录：

```sh
command="$HOME/bin/rrsync <folder>",no-agent-forwarding,no-port-forwarding,no-pty,no-user-rc,no-X11-forwarding ssh-rsa <cert>
```

`<folder>` 是指你的网站目录，比如： `~/public_html/you.org/blog-html/`。

#### 第三步：Rsync（客户端）

在网站源码目录中添加 `deploy` 脚本：

```sh
#!/bin/sh

rsync -crvz --rsh='ssh -p2222' --delete-after --delete-excluded   <folder> <user>@<site>:
```

命令行参数如下：


- `--rsh=ssh -p2222` &mdash; SSH 访问的端口，如果你的主机用了一个非默认的端口则需要设置这个值（如： HostGator ）
- `<folder>` &mdash; 本地输出目录的名称（默认是 `_site` ）
- `<user>` &mdash; 主机账户的用户名
- `<site>` &mdash; 服务器名称

使用这个设置，你可以执行下面的命令：

```sh
rsync -crvz --rsh='ssh -p2222' --delete-after --delete-excluded _site/ hostuser@example.org:
```

不要忘了服务器名称后的一栏 `:` !

#### 第四步（可选）：排除迁移脚本防止被拷贝到输出目录

如果你使用这个教程部署你的网站的话建议你执行这一步，如果你把 `deploy` 脚本放在项目的根目录，
Jekyll 会把它拷贝到输出目录，可以通过设置 `_config.yml` 来改变这一行为。

加入以下行即可：

```yaml
# 不会拷贝到输出目录的文件
exclude: ["deploy"]
```

此外，你可以使用 `rsync-exclude.txt` 文件来控制哪个文件会被发送到你的服务器上。

#### 完成!

现在你可以通过执行 `deploy` 脚本来发布你的网站啦~
如果你的 SSH 证书是[受密码短语保护的](https://martin.kleppmann.com/2013/05/24/improving-security-of-ssh-private-keys.html)，
在执行脚本时你会被要求输入密码。

## Rack-Jekyll

[Rack-Jekyll](http://github.com/bry4n/rack-jekyll/) 是一个部署站点到任意 Rack 服务的简单方法，如 Amazon EC2, Slicehost, Heroku 等。它也可以 [shotgun](http://github.com/rtomakyo/shotgun/), [rackup](http://github.com/rack/rack), [mongrel](http://github.com/mongrel/mongrel), [unicorn](http://github.com/defunkt/unicorn/), and [others](https://github.com/adaoraul/rack-jekyll#readme) 一起运行。

可以阅读 [这篇文章](http://blog.crowdint.com/2010/08/02/instant-blog-using-jekyll-and-heroku.html) 了解如何使用 Rack-Jekyll 部署到 Heroku 。

## Jekyll-Admin for Rails

如果想在 Rails 中维护 Jekyll 站点，[Jekyll-Admin](http://github.com/zkarpinski/Jekyll-Admin) 包含了实现此功能直接可用的代码。详细可查看 Jekyll-Admin 的 [README](http://github.com/zkarpinski/Jekyll-Admin/blob/master/README) 。

## Amazon S3

如果要在 Amazon S3 上托管你的站点，可以使用 [s3_website](https://github.com/laurilehmijoki/s3_website) 。它会推送你的站点到 Amazon S3 上，Amazon S3 跟任意网络服务器一样，却能够动态扩容到几乎无限流量。这种方式适用小流量博客站点，因为你只需要为你使用的流量付费。

## OpenShift

如果你想要在 OpenShift 设备上部署你的网站，可以参考[这篇文档](https://github.com/openshift-quickstart/jekyll-openshift)。

<div class="note">
  <h5>ProTip™: 使用 GitHub Pages 零麻烦托管</h5>
  <p>GitHub Pages 内部由 Jekyll 驱动, 所以如果你想找个零麻烦、零花费解决方案，Github Pages 是托管 <a href="../github-pages/">Jekyll 驱动站点</a>的首选。</p>
</div>

## Kickster

当使用了 Github Pages 不支持的插件时， 可以通过 [Kickster](http://kickster.nielsenramon.com/) 轻松（自动）部署到 Github Pages。

Kickster 提供了一个具有网络最佳实践的基础 Jekyll 项目设置，并且包含了许都可以提升项目整体质量的优化工具。
Kickster 为 Github Pages 提供了全自动、零担忧的部署脚本。

安装 Kickster 非常简单， 只要安装了 gem 包就万事大吉了， 更多详情参见[这里](https://github.com/nielsenramon/kickster#kickster)。
如果你不想使用 gem 包或者新建一个新项目，你可以只是拷贝部署脚本到 [Travis CI](https://github.com/nielsenramon/kickster/tree/master/snippets/travis) 或 [Circle CI](https://github.com/nielsenramon/kickster#automated-deployment-with-circle-ci)。

## Aerobatic

[Aerobatic](https://www.aerobatic.com) 是一个将 Github Pages 功能移植给 Bitbucket 用户的 Bitbucket 扩展。
包括持续部署，通配SSL证书的自定义域名，CDN，基本认证和阶段分支功能。

自动构建和部署 Jekyll 网站和在 Github Pages 上一样简单——将你的修改推送到仓库（除了 `_site` 目录），
然后数秒内自动触发构建，在其高可用、遍布全球的主机服务商部署你构建的网站。
构建过程会均衡安装和执行自定义插件，详情见我们的[Jekyll文档](https://www.aerobatic.com/docs/static-generators#jekyll)。

## PubStorm

[PubStorm](https://www.pubstorm.com) 是由 [Nitrous](https://www.nitrous.io) 建立的免费前端和静态网站发布平台。
PubStorm 被发布为 node 包，可以通过执行命令 `npm install -g pubstorm` 来安装。
你可以通过 `storm signup` 命令来创建一个免费账户。

发布网站需要在项目根目录下执行 `storm init` 然后在提示时输入项目路径时输入 `_site` 作为项目路径，
接着可以执行 `jekyll build` 构建网站并执行 `storm deploy` 来发布你的网站。

Pubstorm 提供一个预设的 CDN、免费自定义域名、SSL证书、回滚、协同合作等功能，欲体验更多功能，[参见 Pubstorm 帮助网站](http://help.pubstorm.com)。

你还可以使用 [Nitrous Jekyll Template](https://www.nitrous.io/quickstarts) 来开发你的 Jekyll 项目并直接部署网站到 Pubstorm，
这是在 Windows 上进行Jekyll开发的不错选择。
