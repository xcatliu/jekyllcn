jekyllcn
========

Forked From [jekyll](https://github.com/jekyll/jekyll).

[jekyllcn](http://jekyllcn.com/) 是 [jekyllrb](http://jekyllrb.com/) 的中文翻译网站。

由于官方文档更新，现在中文文档落后于官方文档，感兴趣的可以来贡献翻译。

## 如何贡献翻译

1. [新建一个 issue](https://github.com/xcatliu/jekyllcn/issues/new)，说明要贡献哪篇文档（可以是落后于官方版本的中文文档，也可以是还没有翻译的文档）
2. fork 之后，修改 `/site/_docs/` 中的对应文档进行翻译，并在本地预览，如果不知道如何在本地启动，可以参考[如何在本地启动](#如何在本地启动)
3. 在 `frontmatter` 中将自己加入到 `translators` 字段
4. 提交一个 pull-request，等待审核

## 如何在本地启动

1. 安装 [bundle](http://bundler.io/)
2. 执行 `bundle install`
3. 执行 `bundle exec rake site:preview`

参考 [contributing](http://jekyllrb.com/docs/contributing/)。

## 项目进度

### 翻译进度



### 基础建设

任务 | 优先级 | 备注
---- | ------ | ------
[x] 跟进官网网站版本 | +++ | 最近一次跟进：2015-06-22
[x] 页脚加上贡献翻译链接 | +++ |
[x] 导航加上贡献翻译链接 | +++ |
[x] 每篇文档加上贡献翻译链接 | ++++ |
[ ] 每篇文章加上原文链接 | +++ |
[x] 加上 ga | ++++ |
[x] 加上适配 jekyllcn 的 css | +++ |
[x] 加上如何贡献翻译的文档 | ++ |
[x] 加上如何本地启动的文档 | ++ |
[x] 加上项目进度的文档 | ++ |
[x] header 中文适配 | + |
[x] 上一节下一节中文适配 | + |
[x] 右侧表头中文适配 | + |
[x] 首页中文适配 | +++++ | 最近一次跟进：2015-06-22
[x] head 中文适配 | ++++ | 影响 SEO，故优先级高
