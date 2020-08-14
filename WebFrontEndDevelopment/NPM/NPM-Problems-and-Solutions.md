# NPM Problems and Solutions

## Node Sass does not yet support your current environment

因为测试/尝鲜 Vue 3 ，把本地开发环境的 Node 更新到了最新。

更新 Node 后创建的新项目使用 Sass 正常。

但公司的项目，就报错 `Node Sass does not yet support your current environment……`，满终端的报错信息。

### 解决方案

卸载问题项目的 node-sass ，再安装至最新版本

```
npm uninstall --save node-sass

npm install --save-dev node-sass
```

```
yarn remove node-sass

yarn add ndoe-sass
```

另外 **不推荐使用 node-sass**，因为该依赖的来源域名是 `github.com`，在国内拉取极其不友好。

**推荐使用 dart-sass。**