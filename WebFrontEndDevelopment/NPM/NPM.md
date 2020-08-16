<!-- vscode-markdown-toc -->
* 1. [安装 依赖/模块](#)
	* 1.1. [npm install 相关命令详解](#npminstall)
* 2. [npm、yarn 查看镜像源地址](#npmyarn)
	* 2.1. [部分镜像源地址：](#-1)
	* 2.2. [使用 cgr 管理/查看 npm 和 yarn 的镜像源地址](#cgrnpmyarn)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->
# NPM

> Node.js 附带的包管理器。



[NPM 官方中文文档](https://www.npmjs.cn/)

实际工作中，个人更推荐使用 yarn 。

能用 yarn 的地方就别用 npm 。反之，亦然。

因为 npm 有时候很（出）玄（问）学（题）。

##  1. <a name=''></a>安装 依赖/模块

- 直接安装（默认安装包仓库最新版本）

    ```npm
    npm install moduleName

    # 明确安装最新版
    npm install moduleName@latest
    ```

- 安装指定版本: ~ + `@` + `版本号`

    ```npm
    npm install moduleName@VersionNumber
    npm install vue-cli@2.9.6
    ```
- 安装只在开发环境中使用的：~ + `--save-dev`
    ```npm
    npm install moduleName --save-dev
    ```

- 安装只在生产环境中使用的：~ + `--save`

    ```npm
    npm install moduleName --save
    ```
- 强制 **重新安装** 模块: ~ + `--force`

    ```npm
    npm install --force
    ```

###  1.1. <a name='npminstall'></a>npm install 相关命令详解

- npm install X:

    - 会把 X 包安装到 node_modules 目录中
    - 不会修改 package.json
    - 之后运行 npm install 命令时，不会自动安装X

- npm install X -–save:

    - 会把 X 包安装到 node_modules 目录中

    - 会在 package.json 的 dependencies 属性下添加 X

    - 之后运行 npm install 命令时，会自动安装X到 node_modules 目录中

    - 之后运行 npm install -–production 或者注明 NODE_ENV 变量值为 production 时，会自动安装 msbuild 到 node_modules 目录中

- npm install X -–save-dev:

    - 会把X包安装到 node_modules 目录中

    - 会在 package.json 的 devDependencies 属性下添加X

    - 之后运行 npm install 命令时，会自动安装 X 到 node_modules 目录中

    - 之后运行npm install –production 或者注明 NODE_ENV 变量值为 production 时，不会自动安装 X 到 node_modules 目录中

使用原则:

运行时需要用到的包使用 -–save，否则使用 -–save-dev。

> -g 、-save 、–save-dev 可以写在 moduleName 前面

> moduleName 可以是多个，用空格间隔

>  --save 可以简写为 -S

> -–save-dev 可以简写为 -D

##  2. <a name='npmyarn'></a>npm、yarn 查看镜像源地址

```sh
npm config get registry  // 查看npm当前镜像源
# https://registry.npmjs.org/   //默认镜像源
npm config set registry https://registry.npm.taobao.org/  // 设置npm镜像源为淘宝镜像

yarn config get registry  // 查看yarn当前镜像源
# https://registry.yarnpkg.com/   //默认镜像源
yarn config set registry https://registry.npm.taobao.org/  // 设置yarn镜像源为淘宝镜像
```

###  2.1. <a name='-1'></a>部分镜像源地址：

- npm：https://registry.npmjs.org/

- yarn：ttps://registry.yarnpkg.com/   //yarn 天下第一

- cnpm：https://r.cnpmjs.org/

- taobao：https://registry.npm.taobao.org/

- nj：https://registry.nodejitsu.com/

- rednpm：https://registry.mirror.cqupt.edu.cn/

- npmMirror：https://skimdb.npmjs.com/registry/

- deunpm：http://registry.enpmjs.org/

###  2.2. <a name='cgrnpmyarn'></a>使用 cgr 管理/查看 npm 和 yarn 的镜像源地址

- 安装

    ```sh
    npm install -g cgr
    ```

-  查询

    ```sh
    cgr ls
    ```

    ```sh
    # 查询
    λ cgr ls

    N npm ---- https://registry.npmjs.org/
      cnpm --- http://r.cnpmjs.org/
      taobao - https://registry.npm.taobao.org/
    Y yarn --- https://registry.yarnpkg.com/
    ```

## 查询当前项目特定依赖的版本号

```npm
npm ls node_modules_name
```

- 若存在该依赖，则返回：依赖名+版本号。

- 若不存在该依赖，则返回 empty。以此可检验是否安装了某依赖。