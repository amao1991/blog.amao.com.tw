---
title: "Hexo #2: deploy on Github Pages which transfers to new machine"
date: 2020-03-17 16:54:24
tags:
  - github
  - hexo
categories: Hexo
---

The website is deploy on Github Pages by Hexo.

It meet some questions when I transfer the source code to new computer as below: 

<!--more-->

<h3>ERROR Deployer not found: git</h3>

```
$ npm install hexo-deployer-git --save
```

<h3>WARM No layout: index.html</h3>

confirm the theme which be used is under the theme folder

I use [icarus](https://github.com/ppoffice/hexo-theme-icarus) theme but the theme/icarus folder is empty

so use the command as below:

```
$ git clone https://github.com/ppoffice/hexo-theme-icarus.git themes/icarus
```

but it will back to default setting

<h3>CNAME</h3>

If the website has cname:

```
$ npm install hexo-generator-cname --save
```
