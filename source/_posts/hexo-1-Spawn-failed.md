---
title: "Hexo #1: Spawn failed"
date: 2019-12-31 16:21:58
tags:
- hexo
- github
categories: Hexo
---

幾個月沒上來要發個文章他就爆了，FINE。

<!--more-->

在下了 `hexo d` 指令後，出了如下圖錯誤

{% asset_img slug 2019-12-31-42001.png %}

兩個問題：

1. 詢問我 Username, Password
2. Spawn failed

首先，原本的 `_config.yml` 如下

```
deploy:
  type: git
  repo: https://github.com/amao1991/blog.amao.com.tw.git
```

改成這樣後，解決了問題一

```
deploy:
  type: git
  repo: git@github.com:amao1991/blog.amao.com.tw.git
  branch: gh-pages
```

資料爬著爬著發現 github 中的 SSH key 沒了，喵的，把 `id_rsa.pub` 塞回去後

原本我 deploy 的指令是

```
hexo clean
hexo g
hexo d
```

改成一起執行

```
hexo clean
hexo g -d
```

以上。