# Vue 3 Start

## 开发环境

**为确保兼容性和支持，请升级/安装你的 Node.js、npm 和 VueCli 至最新**

比如我现在 `2020/8/8`：

```
node,js：14.6.0
npm：6.14.6
VueCli：4.4.6
```

## Start

**注意**

> **目前 Vue 3.0 的项目需要从 Vue 2.x 项目升级而来。** 所以我们得先创建一个的 Vue 2.x 项目。另外记得选好你可能需要的 VueRouter、Vuex 和 SCSS ……，避免在升级 Vue 3 后手动去添加。

 ### 创建 Vue 2.x 项目

    ```
    vue create projectName
    ```

    一如你曾经创建所需的 Vue 2.x 项目一般，在 VueCli 引导程序中根据需求去配置项目。

### 升级为 Vue 3.0 项目

目前在 VueCli 构建 Vue 3.0 项目，需要通过添加插件来升级的方式实现。（用随 Vue 3 项目诞生的 [vite](https://v3.vuejs.org/guide/installation.html#vite) 倒是可以直接构建 Vue 3 项目）

在你需要升级为 Vue 3 框架的项目路径下执行：

```
vue add vue-next
```

执行后，会修改原有的 Vue 2.x 的代码

- 安装 Vue 3.0 依赖
- 更新 Vue 3.0 webpack loader 配置，使其能够支持 .vue 文件构建（这点非常重要）
- 创建 Vue 3.0 的模板代码（目前感觉跟以前没啥区别
- 自动将代码中的 Vue Router 和 Vuex 升级到 4.0 版本，如果未安装则不会升级
- 自动生成/更新为 Vue Router 和 Vuex 4.0 版本模板代码
