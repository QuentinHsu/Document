# Vue Cli

[Vue-cli 官方文档](https://cli.vuejs.org/zh/guide/)

目前有分
- 3.0 及以上（包名：@vue/cli）版本
- 2.x （旧，包名：vue-cli）版本（止步于 [v2.9.6](https://www.npmjs.com/package/vue-cli)）

使用

```vue-cli
npm install -g @vue/cli
# OR
yarn global add @vue/cli
```

建议使用 npm 命令安装 VueCli。因为实测使用 yarn 安装 VueCli 出现了问题。[详情](../ProblemAndSolution/November2019/November27_2019.md)

**只有使用 npm 命令安装的 VueCli 能正常使用。**

**该命令默认直接安装 Vue-cli 的最新版。** 比如现在最新是 `v4.1.0` ，而你想装 `v3.12.0` ：`npm install -g @vue/cli@3.12.0`

截至2019.11，`v4.1.0-beta.0` 。（也就是说，Vue-cli 已经 `v4.x` 了）

[Vue-cli 官方仓库](https://github.com/vuejs/vue-cli/releases)

若是仍想使用 Vue-cli 2.x 构建 Vue 项目，需要这样安装

```vue-cli 2.x
# cli 2.x
npm install -g vue-cli

# 但之后你又想安装 cli 3.x ，则需要注意：
# 3.x 安装时，如果之前安装了 2.x 需要卸载 2.x 再安装

npm install -g @vue/cli
```

**-g**：全局安装。

### 创建项目

- 在 Vue-cli **3.0+** 时

    ```vue-cli
    vue create <projectName>
    ```

    可以通过全局桥接工具，依旧能在 3.x 时使用 2.x 时的命令拉取（构建） 2.x 时的项目模板:

    > Vue CLI >= 3 和旧版使用了相同的 vue 命令，所以 Vue CLI 2 (vue-cli) 被覆盖了。如果你仍然需要使用旧版本的 vue init 功能，你可以全局安装一个桥接工具：

    ```vue-cli 3.0+
    npm install -g @vue/cli-init

    # `vue init` 的运行效果将会跟 `vue-cli@2.x` 的相同
    vue init webpack my-project
    ```

- 在 Vue-cli **2.x** 时

    ```vue-cli
    vue init <templateName> <projectName>
    ```

    \<templateName>：
    1. **webpack** 功能齐全的 Webpack + vue-loader 设置，具有热重载，linting，测试和css提取功能。
    2. **webpack-simple** 一个简单的 Webpack + vue-loader 设置，用于快速原型设计。
    3. **browserify** 全功能的 Browserify + vueify 设置，具有热重载，linting和单元测试功能。
    4. **browserify** 一个简单的 Browserify + vueify 设置，用于快速原型设计。
    5. **pwa** 基于 vue webpack 模板的 pwa 模板
    6. **simple** 最简单的 vue 单页面项目
