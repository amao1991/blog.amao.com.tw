---
title: "Git #1: Specific account for different project in the same computer"
date: 2019-07-11 15:50:18
tags:
- git
categories: Git
---

Multiple git account in the same computer

<!--more-->

## Windows

### Set gitconfig

Global config: default path `C:\Users\Elmo\.gitconfig`

```
[User]
    name = elmo_aaa
    email = elmo@aaa.com

[includeIf "gitdir/i:D:/Note/"]
    path = D:/Note/.git/config
```

Specific project config: `D:/Note/.git/config`

```
[User]
    name = elmo_bbb
    email = elmo@bbb.com
```

### Generate SSH Key for specific account

```
ssh-keygen -t rsa -C "elmo@bbb.com"
```

the default path is `C:\Users\Elmo\.ssh`

> it can't use the default name in the default path because it will replace the original account SSH key

finally, copy the content of public key and paste in GitLab SSH keys