## After clone the blog repository

install usage package

```
npm install
npm install -g node-gyp
```

update submodule theme

```
git submodule update --init --recursive
```

install package from package.json at root dir and themes/[theme]

```
npm install
```

## Add in package.json

```
"hexo-generator-cname": "^0.3.0",
"hexo-deployer-git": "^0.3.1",
"hexo-generator-feed": "^1.2.2",
"hexo-generator-sitemap": "^1.1.2"
```