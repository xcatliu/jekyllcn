jekyllcn
========

Forked from [jekyll](https://github.com/jekyll/jekyll).

网址：[http://jekyllcn.com/](http://jekyllcn.com/)

[jekyllcn](http://jekyllcn.com/) 是 [jekyllrb](http://jekyllrb.com/) 的中文翻译网站。

现已更新到 3.0，然而中文文档落后于官方文档，欢迎参与[贡献翻译](https://github.com/xcatliu/jekyllcn#如何贡献翻译)。

## 如何贡献翻译

1. [新建一个 issue](https://github.com/xcatliu/jekyllcn/issues/new)，说明要贡献哪篇文档（可以是落后于官方版本的中文文档，也可以是还没有翻译的文档）
2. fork 之后，修改 `/site/_docs/` 中的对应文档进行翻译，并在本地预览，如果不知道如何在本地启动，可以参考[如何在本地启动](https://github.com/xcatliu/jekyllcn#如何在本地启动)
3. 注意在 Front Matter 中将自己加入到 `translators` 字段，若无此字段，则添加一个
4. 若要修改 css，请修改 `/site/_sass/_jekyllcn.scss`，新增的 css 以 `.jekyllcn-` 开头，尽量避免破坏 jekyll 的文件
4. 提交一个 pull-request，等待审核

## 如何在本地启动

1. 安装 [bundle](http://bundler.io/)
2. 执行 `bundle install`
3. 执行 `bundle exec rake site:preview`

参考 [contributing](http://jekyllcn.com/docs/contributing/)。

## 如何发布到 jekyllcn.com

1. 执行 `bundle exec rake site:publish`

## 项目进度

总体进度：62 / 78 = 79%

### 翻译进度

- [x] 翻译 home
- [x] 翻译 quickstart
- [x] 翻译 installation
- [x] 翻译 usage
- [x] 翻译 structure
- [x] 翻译 configuration
- [x] 翻译 frontmatter
- [x] 翻译 posts
- [x] 翻译 drafts
- [x] 翻译 pages
- [x] 翻译 static-files
- [x] 翻译 variables
- [ ] 翻译 collections
- [x] 翻译 datafiles
- [x] 翻译 assets
- [x] 翻译 migrations
- [x] 翻译 templates
- [x] 翻译 permalinks
- [x] 翻译 pagination
- [x] 翻译 plugins
- [x] 翻译 extras
- [x] 翻译 github-pages
- [x] 翻译 deployment-methods
- [x] 翻译 continuous-integration
- [x] 翻译 troubleshooting
- [x] 翻译 sites
- [x] 翻译 resources
- [x] 翻译 upgrading
- [x] 翻译 contributing
- [x] 翻译 history

### 更新进度

- [x] 更新 home
- [x] 更新 quickstart
- [x] 更新 installation
- [x] 更新 usage
- [ ] 更新 structure
- [ ] 更新 configuration
- [ ] 更新 frontmatter
- [x] 更新 posts
- [x] 更新 drafts
- [x] 更新 pages
- [x] 更新 static-files
- [ ] 更新 variables
- [x] 更新 collections
- [x] 更新 datafiles
- [x] 更新 assets
- [x] 更新 migrations
- [x] 更新 templates
- [ ] 更新 permalinks
- [ ] 更新 pagination
- [ ] 更新 plugins
- [x] 更新 extras
- [ ] 更新 github-pages
- [ ] 更新 deployment-methods
- [ ] 更新 continuous-integration
- [ ] 更新 troubleshooting
- [ ] 更新 sites
- [ ] 更新 resources
- [ ] 更新 upgrading
- [ ] 更新 contributing
- [x] 更新 history

### 基础建设

- [x] 跟进官方网站版本（2015-06-22）
- [x] 首页中文适配（2015-06-22）
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
