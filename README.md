JekyllCN
========

[![Build Status](https://travis-ci.org/xcatliu/jekyllcn.svg?branch=master)](https://travis-ci.org/xcatliu/jekyllcn)

网址：[http://jekyllcn.com/](http://jekyllcn.com/)

Forked from [Jekyll](https://github.com/jekyll/jekyll).

> [JekyllCN](http://jekyllcn.com/) 是 [Jekyll](http://jekyllrb.com/) 的中文翻译网站。

## 公告

由于官方文档更新，现在中文文档落后于官方文档，欢迎参与[贡献翻译](https://github.com/xcatliu/jekyllcn#如何贡献翻译)。

注意：中文排版遵循这个规范：[写给大家看的中文排版指南](http://zhuanlan.zhihu.com/p/20506092)

注意：暂时放弃了翻译 contributing 和 history，因为他们是脚本生成的

## 如何贡献翻译

1. [新建一个 issue](https://github.com/xcatliu/jekyllcn/issues/new)，说明要贡献哪篇文档（可以是落后于官方版本的中文文档，也可以是还没有翻译的文档），注意翻译之前先看看 issues 里面有没有人已经认领了
2. fork 之后，修改 `/site/_docs/` 中的对应文档进行翻译，并在本地预览，如果不知道如何在本地启动，可以参考[如何在本地启动](https://github.com/xcatliu/jekyllcn#如何在本地启动)
3. 注意在 Front Matter 中将自己加入到 `translators` 字段，若无此字段，则添加一个
4. 注意在 Front Matter 中更新 `update_date`，若无此字段，则添加一个
5. 若要修改 css，请修改 `/site/_sass/_jekyllcn.scss`，新增的 css 以 `.jekyllcn-` 开头，尽量避免破坏 jekyll 的文件
6. 提交一个 pull-request，等待审核

## 如何在本地启动

1. 安装 [bundle](http://bundler.io/)
2. 执行 `bundle install`
3. 执行 `bundle exec rake site:preview`

参考 [contributing](http://jekyllcn.com/docs/contributing/)。

## 如何发布到 jekyllcn.com

使用 Travis CI 自动发布：https://travis-ci.org/xcatliu/jekyllcn

## 项目进度

### 更新进度
- [ ] home
- [x] quickstart (2016-04-19)
- [x] installation (2016-04-19)
- [ ] usage
- [x] structure (2016-04-20)
- [x] configuration (2016-04-20)
- [x] drafts (2016-04-22)
- [x] frontmatter (2016-04-22)
- [x] pages (2016-04-22)
- [ ] static-files
- [x] posts (2016-04-22)
- [x] collections (2016-04-26)
- [ ] datafiles
- [x] assets (2016-04-26)
- [ ] migrations
- [x] templates (2016-04-26)
- [x] variables (2016-04-26)
- [x] permalinks (2016-05-04)
- [x] pagination (2016-05-04)
- [ ] plugins
- [x] extras (2016-05-09)
- [ ] github-pages
- [ ] deployment-methods
- [ ] continuous-integration
- [ ] troubleshooting
- [ ] sites
- [ ] resources
- [x] Theme (2016-05-10)
- [x] upgrading/0-to-2 (2016-05-09)
- [ ] upgrading/2-to-3 (2016-05-10)

### 基础建设

- [x] 跟进官方网站版本 (2016-05-10)
- [x] 首页中文适配 (2016-04-20)
- [x] 页脚加上贡献翻译链接
- [x] 导航加上贡献翻译链接
- [x] 每篇文档加上贡献翻译链接
- [x] 加上 ga
- [x] 加上适配 jekyllcn 的 css
- [x] 加上如何贡献翻译的文档
- [x] 加上如何本地启动的文档
- [x] 加上项目进度的文档
- [x] header 中文适配
- [x] 上一节下一节中文适配
- [x] 右侧表头中文适配
- [x] head 中文适配
- [x] 每篇文文档加上原文链接
- [x] 在 header 中加入贡献翻译链接
- [x] 每篇文档加上翻译贡献者
- [x] 在 header 中底色代表项目进度
- [x] 使用 Travis CI 自动发布
