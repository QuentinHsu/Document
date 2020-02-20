# Vue Development Process

> Vue开发流程

## 搭建开发环境

开发环境：

- Windows 10
  - Node.js
    - npm
      - yarn

其实还需要安装 Git ,因为需要进行版本管理。（不过也看你自身的需求

在安装 [Node.js](https://nodejs.org/zh-cn/download/) 后，会附带安装了 [npm](https://www.npmjs.cn/) 。

我们再使用 npm ，通过命令行的形式全局安装 yarn 。

```npm
npm install -g yarn
```
全局安装，是因为 yarn 会在多个项目中使用。

npm 和 yarn 都是“包管理工具”。个人推荐在开发中使用 yarn 作为开发项目的**主要**包管理工具。

**能用 yarn 的地方，就不要用 npm 。**

相关地址：
- node.js：
  - **安装**：
    - 安装镜像下载地址：[Node.js](https://nodejs.org/zh-cn/)
    - 下载 **长期支持版（LTS）** 就好。
    - **注意**：[Node.js 中文网](http://nodejs.cn/)。这儿下载出来的是文档！！！而且感觉不是 node.js 官方的网站，像是国人的自发项目网站。
  - **更新**：
    - Windows 下，只能通过去上面的提到的 [Node.js](https://nodejs.org/zh-cn/) 下载最新的 LTS 镜像进行覆盖安装以更新 Node.js 版本。
- npm：
  - **安装**：
    - 第一次安装，无需下载额外的安装包和进行安装。因为会随 Node.js 的安装而安装。并且你更新 Node.js 的版本，同时也会更新 npm 的版本。
  - **更新**
    1. 使用命令行进行安装
      ```npm
      npm install -g npm@latest
      ```
    2. 下载安装最新 Node.js ，以更新 npm 。比如 Node.js 长期支持版（LTS）v12.13.1 ,包含 npm v6.12.1。但是，npm 的更新频率比 Node.js 的更新频率高。所以，若需更新使用新版 npm ，请使用命令行进行安装。
- yarn：
  - **安装**：
    - 使用 npm 命令行安装

      ```npm
      npm install -g yarn
      ```
  - **更新**：
    - 使用 npm 命令行更新

      ```npm
      npm install -g yarn@latest
      ```

      ```npm
      npm update -g yarn@latest
      ```

    - 自己更新自己：

      ```npm
      yarn global update yarn@latest
      ```
      （可能无效）

      下面这条命令也“**不起作用**”了

      ```npm
      yarn global add yarn@latest
      ```

      可能你觉得这样可以，但是并不可以（我不要你觉得）：[Yarn cannot update itself by installing itself](../NPM/Yarn/Yarn.md#yarn-cannot-update-itself-by-installing-itself)

## 初始化构建项目

### 准备
  在这，我使用 VueCli 脚手架工具进行构建 Vue 项目，于是需要全局安装 VueCli 。

  VueCli：`v3.12.0`

  ```
  npm install -g @vue/cli@3.12.0
  ```

  为何又要在这使用 npm 安装 VueCli ，而不使用 yarn 呢？详情请看：[实锤！VueCli 只能使用 npm 安装！](../ProblemAndSolution/November2019/November27_2019.md)

  如何查询已安装的 VueCli 版本

  ```vue
  vue -V
  ```

### 开始构建项目

  ```vue
  vue create <projectName>
  cd <projectName>
  ```

### 引入 Element UI

  假如你要在使用 VueCli 3.x 构建的项目中，使用 Element UI ，Element UI 官方提供了一个专门插件：[vue-cli-plugin-element](https://github.com/ElementUI/vue-cli-plugin-element)。详情看其 README 文档。

  ```vue
  vue add element
  ```

  执行该命令即可，相应的引入会自动为你写入相应的文件中

### 去除浏览器默认样式

[normalize.css](https://github.com/necolas/normalize.css)

这个可以引入直接 CSS 文件进行使用，也可以通过 npm / yarn 进行安装使用。

```npm
npm install --save normalize.css
```

```yarn
yarn add normailize.css
```

我是通过 yarn 安装的。

并要在 `src/main.js` 中引入 normalize.css 。

```
import 'normalize.css/normalize.css'
```

不然不会生效。

> ### yarn 安装 normalize.css 失败
> `2020/02/20`
>
> 进行一测试项目的搭建，发现 normalize.css 无法使用 yarn 进行安装，包仓库显示无法找到该包。遂使用 npm 进行安装，报错（着实嫌弃 npm ）。无奈只好添加 normalize.css 独立文件进项目里。并
>
> ```
> # src/main.js
> import '<normalize.css存放路径>'
> ```
> 即可生效!


