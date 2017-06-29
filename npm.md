# npm 相关命令与使用

如果你是国内用户，并且不方便翻墙，建议使用 [cnpm](https://npm.taobao.org/) 作为 npm 的备用品  
安装 cnpm：`sudo npm install cnpm -g --registry=https://registry.npm.taobao.org`  
安装完成后，下面的所以命令，都可以把 npm 换成 cnpm  
另外，如果你既不喜欢 npm 的安装速度，也不想使用 cnpm，那么我建议你使用 [yarn](https://yarnpkg.com/zh-Hans/)  

推荐一个 npm 包：[n](https://github.com/tj/n)，可以用来管理 Node.js版本

### `sudo npm list -g --depth=0`

显示 npm 全局安装包，depth 表示查看依赖的深度

### `sudo npm uninstall -g  moudleName`

卸载某个 node 全局模块

### `sudo npm update -g moudleName`

更新某个 node 全局模块

### `npm config get prefix`

获取当前设置的目录

### `sudo npm install npm@4.4.4 -g`

升级 npm 到固定版本号  
如果你已经安装某个版本，想替换版本号，也可以使用这个命令

### `npm -g outdated`

查看那些包可以更新

### `npm install --only=production`

只安装 dependencies 里面列出的模块

### `npm init -y`

快速生成 `package.json` 文件

### 发布版本

- 升级补丁版本号：`npm version patch`
- 升级小版本号：`npm version minor`
- 升级大版本号：`npm version major`
- 升级到版本号「消息、发布」

```sh
npm version 0.3.2 -m "…"
npm publish
```