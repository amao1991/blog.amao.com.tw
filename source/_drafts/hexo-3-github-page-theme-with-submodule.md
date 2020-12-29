---
title: "Hexo #3: 用 git submodule 管理主題"
tags:
  - github
  - hexo
categories: Hexo
---

有鑒於上次換機器時，重新部署搞了半天，最後又都用些牛頭不對馬尾（當初用 submodule 重新部署時卻直接 clone 下來）的方式處理掉

<!--more-->

## npm install 在做什麼

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

## 用 git submodule 管理主題

先將想要的主題 fork 到自己的 github，用 submodule 的方式加入 blog 的 repository

```
git submodule add https://github.com/amao1991/hexo-theme-next.git themes/next
```

## 