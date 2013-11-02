---
layout: docs
title: 创建页面
prev_section: drafts
next_section: variables
permalink: /docs/pages/
contributor: sdpfoue
---

作为[写文章](../posts/)的补充，Jekyll 还可以创建静态页面。
利用 Jekyll 带来的便利，你只需要复制文件或文件夹，就是这么简单。

## 主页

像任何网站的配置一样，需要按约定在站点的要目录下找到 `index.html` 文件，
这个文件将被做为主页显示出来。除非你的站点设置了其它的文件作为默认文件，
这个文件就将是你的 Jekyll 生成站点的主页。

<div class="note">
  <h5>提示™: 在主页上使用布局</h5>
  <p>
    站点上任何 HTML 文件，包括主页，都可以使用布局和 include 中的内容一般共用的内容，如页面的 header 和 footer. 将合适的部分抽出放到布局中。
  </p>
</div>

## 其它的页面的位置

将 HTML 文件放在哪里取决于你想让它们如何工作。有两种方式可以创建页面：

- 命名 HTML 文件：将命名好的为页面准备的 HTML 文件放在站点的根目录下。
- 命名文件夹：在站点的根目录下为每一个页面创建一个文件夹，并把 index.html 文件放在每
  个文件夹里。

这两种方法都可以工作（并且可以混合使用），它们唯一的区别就是访问的 URL 样式不同。

### 命名 HTML 文件

增加一个新页面的最简单方法就是把给 HTML 文件起一个适当的名字并放在根目录下。
一般来说，一个站点下通常会有：主页 (homepage), 关于 (about), 和一个联系 (contact)
页。根目录下的文件结构和对应生成的 URL 会是下面的样子：

{% highlight bash %}
.
|-- _config.yml
|-- _includes/
|-- _layouts/
|-- _posts/
|-- _site/
|-- about.html    # => http://yoursite.com/about.html
|-- index.html    # => http://yoursite.com/
└── contact.html  # => http://yoursite.com/contact.html
{% endhighlight %}

### 命名一个文件夹并包含一个 index.html 文件

上面的方法可以很好的工作，但是有些人不喜欢在 URL 中显示文件的扩展名。用 Jekyll 达
到这种效果，你只需要为每个顶级页面创建一个文件夹，并包含一个 `inex.html` 文件。
这样，每个 URL 就将以文件夹的名字作为结尾，网站服务器会将对应的 index.html
展示给用户。下面是一个示例来展示这种结构的样子：

{% highlight bash %}
.
├── _config.yml
├── _includes/
├── _layouts/
├── _posts/
├── _site/
├── about/
|   └── index.html  # => http://yoursite.com/about/
├── contact/
|   └── index.html  # => http://yoursite.com/contact/
└── index.html      # => http://yoursite.com/
{% endhighlight %}

这种方式可能不适合每个人，对那些喜欢干净 URL 的人这是一种简单有效的方法。
最终选择哪种方法完全由你来决定！
