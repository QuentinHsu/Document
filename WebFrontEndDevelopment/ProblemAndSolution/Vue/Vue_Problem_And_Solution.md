# Vue Problem and Solution

## 在构建项目后遇如下报错，并提示运行“npm rebuild node-sass”

``` node
Module build failed (from ./node_modules/sass-loader/dist/cjs.js):
Error: Missing binding E:\WebPersonalProject\Blog\blog2\node_modules\node-sass\vendor\win32-x64-64\binding.node
Node Sass could not find a binding for your current environment: Windows 64-bit with Node.js 10.x

Found bindings for the following environments:
  - Windows 64-bit with Node.js 10.x

This usually happens because your environment has changed since running `npm install`.
Run `npm rebuild node-sass` to download the binding for your current environment.
```

但运行 `npm rebuild node-sass` 失败，应该是因为这命令走的是 github.com 域名下载。（但我未能让 node/npm 走代理，所以走不通）

```npm
λ npm rebuild node-sass

> node-sass@4.13.0 install E:\WebPersonalProject\Blog\blog2\node_modules\node-sass
> node scripts/install.js

Downloading binary from https://github.com/sass/node-sass/releases/download/v4.13.0/win32-x64-64_binding.node
```

于是通过查询资料，算是误打误撞（跟网上提供的方案不尽相同）地找到个“解决方案”：

- **先卸载 node-sass**

    ```npm
    npm uninstall node-sass
    ```

  （卸载过程是真的慢……）

 - **使用 yarn 安装 node-sass**

    ```yarn
    yarn add node-sass
    ```

  **至此，node-sass 成功安装。运行 `yarn serve` ,也不再出现相关报错。**

  此后特地查了下我的 yarn 镜像源地址，是：https://registry.yarnpkg.com。

  （我还以为是我之前有把 yarn 的镜像源地址换成了淘宝的呢，结果依旧是默认的 yarn 官方镜像源地址）

  还是 yarn 好用！给力！

  我在未完成这个解决方案之前，还专门 npm 安装 sass 时 指定了淘宝镜像地址：

  ```npm
  npm config set sass_binary_site https://npm.taobao.org/mirrors/node-sass/
  ```

  结果执行 `npm rebuild node-sass`，直接不响应。不报错也不解析命令，执行命令后稍微停顿了一下就跳行了。