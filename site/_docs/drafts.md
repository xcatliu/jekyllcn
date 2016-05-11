---
layout: docs
title: 使用草稿
permalink: /docs/drafts/
translators: [yizeng, LeuisKen, TimoTokki]
update_date: 2016-04-22
---

草稿是没有日期的文章。它们是你还在创作中而暂时不想发表的文章。想要开始使用草稿，你需要在网站根目录下创建一个名为 `_drafts` 的文件夹（如在[目录结构](/docs/structure/)章节里描述的），并新建你的第一份草稿：

{% highlight text %}
|-- _drafts/
|   |-- a-draft-post.md
{% endhighlight %}

为了预览你拥有草稿的网站，运行带有 `--drafts` 配置选项的 `jekyll serve` 或者 `jekyll build`。此两种方法皆会将该草稿的修改时间赋值给草稿文章，作为其发布日期，所以你将看到当前编辑的草稿文章作为最新文章被生成。
