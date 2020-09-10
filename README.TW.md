### [English](README.EN.md) | [简体中文](README.md)

JekyllCN
========

[![Build Status](https://travis-ci.org/xcatliu/jekyllcn.svg?branch=master)](https://travis-ci.org/xcatliu/jekyllcn)

網址：[http://jekyllcn.com/](http://jekyllcn.com/)

Forked from [Jekyll](https://github.com/jekyll/jekyll).

> [JekyllCN](http://jekyllcn.com/) 是 [Jekyll](http://jekyllrb.com/) 的中文翻譯網站。

## 公告

由於官方文檔更新，現在中文文檔落後於官方文檔，歡迎參與[貢獻翻譯](https://github.com/xcatliu/jekyllcn#如何貢獻翻譯)。

註意：中文排版遵循這個規範：[寫給大家看的中文排版指南](http://zhuanlan.zhihu.com/p/20506092)。暫時放棄了翻譯 contributing 和 history，因為他們是腳本生成的。

## 如何貢獻翻譯

1. [新建壹個 issue](https://github.com/xcatliu/jekyllcn/issues/new)，說明要貢獻哪篇文檔（可以是落後於官方版本的中文文檔，也可以是還沒有翻譯的文檔），註意翻譯之前先看看 issues 裏面有沒有人已經認領了
2. fork 之後，修改 `/site/_docs/` 中的對應文檔進行翻譯，並在本地預覽，如果不知道如何在本地啟動，可以參考[如何在本地啟動](https://github.com/xcatliu/jekyllcn#如何在本地啟動)
3. 註意在 Front Matter 中將自己加入到 `translators` 字段，若無此字段，則添加壹個
4. 註意在 Front Matter 中更新 `update_date`，若無此字段，則添加壹個
5. 若要修改 css，請修改 `/site/_sass/_jekyllcn.scss`，新增的 css 以 `.jekyllcn-` 開頭，盡量避免破壞 jekyll 的文件
6. 提交壹個 pull-request，等待審核

## 如何在本地啟動

1. 安裝 [bundle](http://bundler.io/)
2. 執行 `bundle install`
3. 執行 `bundle exec rake site:preview`

參考 [contributing](http://jekyllcn.com/docs/contributing/)。

## 如何發布到 jekyllcn.com

使用 Travis CI 自動發布：https://travis-ci.org/xcatliu/jekyllcn

## 如何同步最新的 Jekyllrb

```shell
git remote add jekyllrb git@github.com:jekyll/jekyll.git
git fetch jekyllrb master
git merge jekyllrb/master
# 解決沖突
```

## 項目進度

### [項目進度匯總](http://jekyllcn.com/help/jekyllcn/info-of-docs/)

### 基礎建設

- [x] 跟進官方網站版本 (2016-05-10)
- [x] 首頁中文適配 (2016-04-20)
- [x] 頁腳加上貢獻翻譯鏈接
- [x] 導航加上貢獻翻譯鏈接
- [x] 每篇文檔加上貢獻翻譯鏈接
- [x] 加上 ga
- [x] 加上適配 jekyllcn 的 css
- [x] 加上如何貢獻翻譯的文檔
- [x] 加上如何本地啟動的文檔
- [x] 加上項目進度的文檔
- [x] header 中文適配
- [x] 上壹節下壹節中文適配
- [x] 右側表頭中文適配
- [x] head 中文適配
- [x] 每篇文文檔加上原文鏈接
- [x] 在 header 中加入貢獻翻譯鏈接
- [x] 每篇文檔加上翻譯貢獻者
- [x] 在 header 中底色代表項目進度
- [x] 使用 Travis CI 自動發布
