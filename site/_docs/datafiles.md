---
layout: docs
title: 数据文件
permalink: /docs/datafiles/
translators: yzyzsun
hash: 5647b91
---

除了 Jekyll 的[内建变量](../variables/)之外，你还可以指定用于 [Liquid 模板系统](https://wiki.github.com/shopify/liquid/liquid-for-designers) 的自定义数据。

Jekyll 支持从 `_data` 目录下的 [YAML](http://yaml.org/)、[JSON](http://www.json.org/) 和 [CSV](https://en.wikipedia.org/wiki/Comma-separated_values) 载入数据，注意 CSV 文件**必须**包含表头行。

这个强大的特性可以帮你避免模板中的重复，并能在不修改 `_config.yml` 的情况下设置网站特定的选项。

插件和主题也可以通过数据文件来配置变量。

## 数据目录

正如在[目录结构](../structure/)中所描述的，`_data` 目录用于存储供 Jekyll 生成网站的附加数据。这些文件可以使用 `.yml`、`.yaml`、`.json`、`csv` 扩展名，并可通过 `site.data` 访问。

## 示例：成员列表

这是一个数据文件的简单示例，用以避免在模板中复制粘贴大段代码。

`_data/members.yml`:

{% highlight yaml %}
- name: Tom Preston-Werner
  github: mojombo

- name: Parker Moore
  github: parkr

- name: Liu Fengyun
  github: liufengyun
{% endhighlight %}

或 `_data/members.csv`:

{% highlight text %}
name,github
Tom Preston-Werner,mojombo
Parker Moore,parkr
Liu Fengyun,liufengyun
{% endhighlight %}

这些数据可以通过 `site.data.members` 访问（注意文件名决定了变量名）。

你现在可以在模板中使用该成员列表了：

{% highlight html %}
{% raw %}
<ul>
{% for member in site.data.members %}
  <li>
    <a href="https://github.com/{{ member.github }}">
      {{ member.name }}
    </a>
  </li>
{% endfor %}
</ul>
{% endraw %}
{% endhighlight %}

## 示例：组织结构

数据文件也可以被放在 `_data` 的子目录下，每层目录都将添加进变量的命名空间。下面的示例展示了如何在 `orgs` 目录下分别定义 GitHub 的组织结构：

`_data/orgs/jekyll.yml`:

{% highlight yaml %}
username: jekyll
name: Jekyll
members:
  - name: Tom Preston-Werner
    github: mojombo

  - name: Parker Moore
    github: parkr
{% endhighlight %}

`_data/orgs/doeorg.yml`:

{% highlight yaml %}
username: doeorg
name: Doe Org
members:
  - name: John Doe
    github: jdoe
{% endhighlight %}

该组织结构能够通过 `site.data.orgs` 加上各自的文件名访问：

{% highlight html %}
{% raw %}
<ul>
{% for org_hash in site.data.orgs %}
{% assign org = org_hash[1] %}
  <li>
    <a href="https://github.com/{{ org.username }}">
      {{ org.name }}
    </a>
    ({{ org.members | size }} members)
  </li>
{% endfor %}
</ul>
{% endraw %}
{% endhighlight %}

## 示例：访问特定的作者

页面和文章也可以访问特定的数据项目，下面的例子展示了如何实现：

`_data/people.yml`:
{% highlight yaml %}
dave:
    name: David Smith
    twitter: DavidSilvaSmith
{% endhighlight %}

然后可在文章的头信息中指定作者：

{% highlight html %}
{% raw %}
---
title: sample post
author: dave
---

{% assign author = site.data.people[page.author] %}
<a rel="author"
  href="{{ author.twitter }}"
  title="{{ author.name }}">
    {{ author.name }}
</a>

{% endraw %}
{% endhighlight %}
