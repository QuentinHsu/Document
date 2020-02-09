# Yarn

[Yarn 官方中文文档](https://yarnpkg.com/zh-Hans/docs/cli/)

## 安装

## 更新

请这样，对 yarn 进行更新：

- 使用 npm 对 yarn 更新

  - 真正的更新

      ```npm
      npm update -g yarn
      ```

  - 覆盖安装以更新

    ```npm
    npm install -g yarn
    ```

- 使用 yarn 真正地更新它自己

    ```yarn
    yarn global upgrade yarn
    ```

不要使用 yarn 去安装它自己来更新。因为……

### Yarn cannot update itself by installing itself

> Yarn 不能自己更新自己

- 试图使用 `yarn global upgrade yarn` 更新 yarn
结果：

  无法使用 `yarn global upgrade yarn` 更新 yarn，虽然执行完命令后显示了 `success`
  （执行该命令的时候， yarn 最新版本号为 v1.21.1，非本地）

  ```yarn
  λ yarn global upgrade yarn
  yarn global v1.19.2
  [1/4] Resolving packages...
  [2/4] Fetching packages...
  [3/4] Linking dependencies...
  [4/4] Rebuilding all packages...
  success Saved lockfile.
  success Saved 0 new dependencies.
  Done in 0.19s.
  ```

  继而查询验证本地安装的 yarn 版本

  ```yarn
  λ yarn
  yarn install v1.19.2
  [1/4] Resolving packages...
  success Already up-to-date.
  Done in 0.98s.
  ```

  其实我这时应该使用

  ```yarn
  yarn --version
  λ yarn --version
  1.21.1
  ```

  根据终端的提示，此时 yarn global upgrade yarn 命令它解析到的 yarn 最新版本号就是 v1.19.2，即我本地安装的版本。

  但在我使用 `yarn install --force` 重新拉取依赖时，终端中却提醒我该更新 yarn 的版本了:

  ```yarn
  warning Your current version of Yarn is out of date. The latest version is "1.21.1", while you're on "1.19.2".
  ```

  太憨了……



- 尝试使用 `yarn global add yarn@latest` 更新 yarn

  结果：同样是不成功/无效的

  不信？那你就看下面！

  ```yarn
  D:\Program Files\cmder
  λ yarn global add yarn@latest
  yarn global v1.19.1
  [1/4] Resolving packages...
  [2/4] Fetching packages...
  [3/4] Linking dependencies...
  [4/4] Building fresh packages...
  success Installed "yarn@1.19.2" with binaries:
        - yarn
        - yarnpkg
  Done in 6.11s.
  D:\Program Files\cmder
  λ yarn
  yarn install v1.19.1
  [1/4] Resolving packages...
  success Already up-to-date.
  Done in 0.10s.
  ```

  此时我猜测，可能装到到了当前目录，即命令执行的所在目录（可我明明用的是 `yarn global` 啊，yarn 官方文档所说的全局安装命令格式）。

  于是我跑资源管理器查看当前目录，果不其然！

  当前目录下，多了些东西：

  ```sh
  - node-modules
    - .yarn-integrity
  - yarn.lock
  ```
