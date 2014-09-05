---
layout: docs
title: 使用草稿
prev_section: posts
next_section: pages
permalink: /docs/drafts/
contributor: yizeng
---

草稿是没有日期的文章。它们是你还在创作中而暂时不想发表的文章。想要开始使用草稿，你需要在网站根目录下创建一个名为 `_drafts` 的文件夹（如在[目录结构](/docs/structure/)章节里描述的），并新建你的第一份草稿：

{% highlight text %}
|-- _drafts/
|   |-- a-draft-post.md
{% endhighlight %}

为了预览你拥有草稿的网站，运行 `jekyll serve` 或者带有 `--drafts` 配置选项的 `jekyll build`。此两种方法皆会将 `Time.now` 的值赋予草稿文章，作为其发布日期，所以你将看到草稿文章作为最新文章被生成。
