# webpack

webpack 不会更改你的代码中除 import/export 以外的部分。如果你在使用其它 ES2015 特性，请确保你使用了一个像是 Babel 或 Bublé 的转译器

npm script 会现在本地模块寻找相应的包
比如 package.json，会先在当前目录寻找 `link` 包

```JS
...
"scripts": {
  "lint": "eslint ./src"
...
```

不推荐全局安装 webpack。这会锁定 webpack 到指定版本，并且在使用不同的 webpack 版本的项目中可能会导致构建失败