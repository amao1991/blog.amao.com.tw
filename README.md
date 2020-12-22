## After clone the blog repository

install package from package.json

```
npm install
```

update submodule theme

```
git submodule update --init --recursive
```

at themes/[theme]

```
npm install
```

## Add in `package.json`

```
"hexo-generator-cname": "^0.3.0",
"hexo-deployer-git": "^0.3.1",
"hexo-generator-feed": "^1.2.2",
"hexo-generator-sitemap": "^1.1.2"
```