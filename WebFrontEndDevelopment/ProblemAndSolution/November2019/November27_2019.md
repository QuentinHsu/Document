# 实锤！VueCli 只能使用 npm 安装！

虽然使用 yarn 也能安装，并能显示：

```sh
success Installed "@vue/cli@4.0.5" with binaries:
      - vue
```
但使用命令

```sh
# 查询 VueCli 版本
vue -V      # 没错，最后这个字母，是大写 V ，不是小写 v
# OR
vue --version
```

依旧查不到 VueCli 版本信息！

假如你同时用 npm 指定安装了个 `v3.12.1`，而用 yarn 直接安装了最新版（比如现在最新是 `v4.0.5`）。（为了测试我的某种设想）
此时使用 `vue -V / vue --version` 查询到是 `v3.12.1`。
此时卸载了 npm 安装的 VueCli ，仅剩 yarn 安装的 VueCli。再进行查询 VueCli

```sh
λ vue -V
'vue' 不是内部或外部命令，也不是可运行的程序
或批处理文件。
```

```sh
λ vue --version
'vue' 不是内部或外部命令，也不是可运行的程序
或批处理文件。
```
其实用一条命令检验就够了。因为 `vue -V` = `vue --version`。具体的命令介绍，可以使用在成功安装好 VueCli 后，执行以下命令进行查看

```sh
vue
```

由此可见…… 你懂的。

而 VueCli 官方文档中却介绍可以使用 yarn 命令安装。但……现实情况，并不是我们所想的那样。

（玄学问题，太玄了……）

等有空，我要去 VueCli GitHub 仓库提 issue ！

当 用 VueCli `v3.12.1` 构建（拉取） Vue 项目模板时，

```sh
λ vue create vue_template
?  Your connection to the default yarn registry seems to be slow.
   Use https://registry.npm.taobao.org for faster installation? [Yes/No]
```

卑微的 npm …… 卑微的……

等等！

> ?  Your connection to the default yarn registry seems to be slow.

“yarn”？What？!

我明明用的是 npm 安装的 VueCli 啊！哪怕是 yarn 没安装成功（虽显示 success *** ，但查询不到对应的版本号），我也是照常执行了 yarn 对 VueCli 的卸载啊！

几个意思？！

另外，在这条项目选择提示中，选择 Yes 。不会对 yarn 的镜像源地址造成更改，对 npm 的也一样（亲自查询验证过）。我猜只是 拉取 webpack 模板的临时链接设置。

而且要在下一步，才选择包管理器：

```sh
? Pick the package manager to use when installing dependencies:
*Yarn
 NPM
```

更加让我匪夷所思。