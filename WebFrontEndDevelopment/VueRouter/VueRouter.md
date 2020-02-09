# VueRouter

> 这是个好东西
>
> 虽然我花了两天左右才入门，就因为搞混了个东西……
>
> 说真的 我觉得官方文档写的不是很让人能看懂（或许是我太笨了

## 1. 安装和基本的使用

因为我是基于 Vue.js + VueCli + VueRouter 开发，使用 yarn 作为 包管理工具

所以
- 为项目安装 VueRouter 依赖包

```yarn
yarn add vue-router
```

- 并在项目中的 main.js 中

  ```JavaScript
  import Vue from 'vue'   // 加载全局都会使用的组件时，都要引入 Vue
  import VueRouter from 'vue-router' // 引入 VueRouter

  import App from './App.vue'
  // 引入需要在路由中使用的 Vue 组件
  import index from './component/index.vue'
  import HelloWorld from './component/HelloWorld.vue'

  Vue.config.productionTip = false
  // 加载 VueRouter
  Vue.use(VueRouter)


  // 配置 路由实例
  const router = new VueRouter({  // 注意，这一行的 第二个单词 是 router
  routes: [    // 而 这一行的 第一个单词 是 routes
    {
        path: '/',
        name: 'index',
        component: index
    },
    {
      path: '/helloWorld',
      name: 'helloWorld',
      component: HelloWorld
    }
  ]
  })
  // 创建和挂载根实例。
  // 记得要通过 router 配置参数注入路由，
  // 从而让整个应用都有路由功能
  new Vue({
    router,     // 这儿是 router ！
    // 等同于 router: router
    render: h => h(App),
  }).$mount('#app')
  ```

- 并在 App.vue 中，留坑

  ```vue
  <template>
      <div>
          <router-view></router-view>  // 坑位在此。
      </div>
  </template>
  ```
  值得一提的是，在 `<router-view>(也就是这儿)</router-view>`中所写的内容，并不会显示在页面上。

这样 index.vue 之类的组件 就能通过 `<router-view>` 在 App.vue 组件 上显示，最终展示在 index.html 上。