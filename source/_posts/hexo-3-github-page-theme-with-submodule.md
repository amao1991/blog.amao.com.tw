---
layout: drafts
title: 'Hexo #3: 用 git submodule 管理主題'
tags:
  - github
  - hexo
categories: Hexo
date: 2020-12-30 12:45:42
---


有鑒於上次換機器時，重新部署搞了半天，最後又都用些牛頭不對馬尾（當初用 submodule 重新部署時卻直接 clone 下來）的方式處理掉

<!--more-->

## Npm install 在做什麼

> npm version: 6.14.8

安裝路徑下 `package.json` 中的套件，全部裝在 `node_modules/` 中

以 Hexo 來說，自己加了 cname, git, feed 和 sitemap

```
{
  "name": "hexo-site",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "build": "hexo generate",
    "clean": "hexo clean",
    "deploy": "hexo deploy",
    "server": "hexo server"
  },
  "hexo": {
    "version": "5.3.0"
  },
  "dependencies": {
    "hexo": "^5.0.0",
    "hexo-generator-cname": "^0.3.0",
    "hexo-deployer-git": "^0.3.1",
    "hexo-generator-feed": "^1.2.2",
    "hexo-generator-sitemap": "^1.1.2",
    "hexo-generator-archive": "^1.0.0",
    "hexo-generator-category": "^1.0.0",
    "hexo-generator-index": "^2.0.0",
    "hexo-generator-tag": "^1.0.0",
    "hexo-renderer-ejs": "^1.0.0",
    "hexo-renderer-marked": "^3.0.0",
    "hexo-renderer-stylus": "^2.0.0",
    "hexo-server": "^2.0.0",
    "hexo-theme-landscape": "^0.0.3"
  }
}
```

因為我的 local 平常不會放部落格的 repository，部落格相關的 module 也沒安裝在 global，需要更新時才從 github 上 clone 下來，並下 `npm install` 指令依照 `package.json` 的內容安裝相關 modules。

## 用 git submodule 管理主題

### Git submodule add

先將想要的主題 fork 到自己的 github，用 submodule 的方式加入 blog 的 repository

```
git submodule add https://github.com/amao1991/hexo-theme-next.git themes/next
```

git 會用 hash 紀錄所使用的 submodule 版本

{% asset_img submodule_hash.png %}

### Update theme

> 這邊使用了偷吃步的方式...

直接先 clone 主題的 repository，編輯後 push 上去，再去 clone 部落格的 repository，這時主題的路徑下是空的，先更新主題

```
// 根據已註冊的 submodule 進行更新
git submodule update --init --recursive
// 如果要用的主題版本和原本註冊的不同 (hash 不同)，把新的主題拉下來
git pull origin master
```

{% asset_img pull_theme.png %}

更新完 submodule 後，部落格本身的 repository 也需要 commit (因為改了 submodule 的 hash)

{% asset_img theme_new_commit.png %}

## Conclusion

偷吃步的部分，要記得補回來 QwQ

## Reference

[1] [Git Submodule 用法筆記](https://blog.chh.tw/posts/git-submodule/)