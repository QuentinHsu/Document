# 个人项目中的 Git 和 “远程 Git 仓库” 使用

在本地使用 Git ，对你的项目文件进行版本管理

## Git的安装

我觉得不用我再介绍这个了...

## 新建文件夹

若是你的项目还未开始/正要开始，那么我们就新建一个文件夹，作为项目的本地存放专属地址，也是我们的使用 Git 中所称的“仓库”所待的地方。Origin！

Windows用户：
    - 图形化创建，这个就不用我再描述如何创建新文件夹吧
    - 命令行

      ```bash
      mkdir fileName
      ```

Linux：

```bash
mkdir fileName
```

> **温馨提示** 🌈
>
> 该文件夹的名称是**可以修改**的。
>
> 比如，你这个项目之前是叫：`SmallStar`，现在又想换一个项目名字，叫`BigSart`。
>
> **请放心大胆的换！**
>
> 不会影响你的 Git 使用，哪怕是你之后链接/关联了软件源代码托管服务平台（GitHub，[Gitee](https://gitee.com)）的远程仓库，也不会有丝毫影响。比如，你可能会以为：更改了本地这个 “根目录文件名” ，会同时更改软件源代码托管服务平台（）的远程仓库名/影响了本地仓库和远程仓库的链接关联（😜放心，这个是完全不会发生的事情）。

## 初始化仓库

```bash
git init
```

在你项目根目录运行该命令后，该目录则会初始化成一个仓库

## 查看仓库当前状态

```bash
git status
```

## 暂存

```bash
git add
git add . #1
git add fileName
```

#1 处的 `.` 是 通配符 ，指当前路径下的所有文件（不包括已被删除的文件哟）。

## 提交

```bash
git commit

git commit -m '提交信息'

git commit -m "提交信息"
```

Windows下，你在写 "提交信息" 内容时，且想使用英文：

1. 使用单引号包围 "提交信息" 内容，你需要在单词之间使用下划线（`_`）来间隔,不然直接使用空格来间隔单词，运行命令会报错。
2. 使用双引号包围 "提交信息" 内容，则不需要添加下划线，直接用空格间隔单词就好。

然而……我又发现有例外：Git 软件版本同样是 `2.24.0.windows.2` ，不管是在哪个终端里，在我的电脑（Widnows 10 1903）上会100%复现这个问题，然而在我公司的电脑上（Windows 10 1703）这完全不会有这问题，单双引号，都可以正常使用。很迷……

为了不影响 Coding 带来的愉悦（看到 error 就烦），**建议，在 Windows 平台使用双引号。**

(使用 macOS 和 Linux 就会不有这种“阻碍”╮(╯-╰)╭)

### 修改上一次提交信息

```bash
git commit --amend
```

执行后，将会弹出修改界面。修改完成后关闭该页面，即修改成功，并重新生成新的commit（或者说是覆盖掉“无用”的 commit 信息）。

## 本地 Git 仓库和远程仓库的关联

**注意**：这儿的指的“远程仓库”，是指的你自己的 GitHub 账户下的仓库（自己创建的和 fork 的仓库），不是别人的仓库！

我们来把本地 Git 仓库和远程 Git 仓库（我在这里是用 GitHub ）它俩之间建立起一个联系：

1. 假如你是先在GitHub上创建了一个远程仓库，那么我们只需要在本地 clone 一下即可。在你准备存放Git仓库的目录下运行一下命令：

    ```bash
    git clone 你的远程仓库SSH/HTTPS链接
    ```

    至此，你的本地仓库已与远程仓库“默认”建立了联系。
    **该命令默认只会 clone 远程仓库 master 分支下的内容。并不会 clone 整个仓库（假如这个仓库除了 master 分支外还有其他分支的话）下来**

    若是想 clone 某一指定分支

    ```bash
    git clone -b <分支名> SSH/HTTPS
    ```

    **注意**：
    >假如你在本地专门创建了一个为这个仓库存放的文件夹，比如远程仓库名叫 “abc” ，然后你在本地创建了一个 “ABC” 的文件夹，那么你在 “ABC” 文件夹目录下运行 clone 命令之后，你的 “ABC” 文件夹下就会多出一个 “abc” 文件夹（这文件夹里面才是整个远程仓库的文件）。这可能跟你 clone 之前想的文件存放不太一样，所以根据你的习惯/需要，选定 clone 的本地目录。
2. 假如你已在本地创建了一个仓库，那么我们需要新建一个空的远程仓库，然后把远程仓库的链接“添加”到本地仓库。

    1. 如何新建远程仓库，我就不介绍了。
        - 假如你想在远程仓库添加许可，建议：先创建远程仓库并 clone 到本地才开始开发。不然你很可能再添加远程仓库链接到本地仓库，却 push 不上去。（我目前就遇到这种情况，貌似只能先如我说的这样才行）
    2. 添加远程仓库链接到本地仓库。

        ```bash
        git remote add 仓库名 你的远程仓库HTTPS/SSH链接

        git remote add origin 你的远程仓库HTTPS/SSH链接

        git remote add 自己定义远程仓库名 你的远程仓库HTTPS/SSH链接
        ```

        关于 自定义远程仓库名 ：
        >该自定义仓库名，在你提交上传到远程仓库时，输入上传代码时（如：git push origin master），origin 要替换成你自定义的仓库名，否则无法上传。
        >
        >注意：这儿的自定义远程仓库名，不是远程仓库在远程仓库托管平台上的名字！而是你在本地给它取的名字。**所以为避免你的遗忘/搞混影响工作，可以统一命名为“origin”。** 不过也还是可以通过 `git status` 查询当前仓库的信息，来查看当前仓库的（自定义）本地仓库名。
    3. 提交本地已有的代码。

        假如你直接
        ```bash
        git push
        ```
        会得到如下提示

        ```bash
        λ git push
        fatal: The current branch master has no upstream branch.
        To push the current branch and set the remote as upstream, use

        git push --set-upstream origin master
        ```

        根据提示，你需要执行

        ```bash
        git push --set-upstream origin master
        ```
        照做就好。

        命令执行后会“自动” push 。再这之后，你就可以正常地使用 `git push` 。因为这时，你的本地仓库才与远程仓库建立“正常”的联系。

HTTPS 和 SSH 的区别：

1. 前者可以随意克隆 GitHub 上的项目，而不管是谁的；而后者则是要求你必须是你要克隆的项目的拥有者或管理员，且需要先添加 SSH key ，否则无法克隆。
2. HTTPS url 在 push 的时候是需要验证用户名和密码的；而 SSH 在 push 的时候，是不需要输入用户名的，如果配置 SSH Key 的时候设置了密码，则需要输入密码的，否则直接是不需要输入密码的。(假如在生成 SSH Key的时候设置了密码，以为了一定情况下的安全（因为你在 push 时候需要输入生成 SSH Key 时设置的密码，并非是你的远程仓库平台账户密码），也总比使用 HTTPS 时，输入两次内容要方便得多)

所以，·**推荐使用 SSH ，后面能少很多事情**

## 接下来才是“重（难）点”

**约定**：

若无特殊说明

1. 如下所有内容的操作都在你 **本地仓库的当前路径下进行操作**（其实上面的也是）
2. **本地仓库名默认都叫 “origin”**

## 上传本地仓库内容到远程仓库

若是本地只有 `master` 这一个分支，就直接

```bash
git push
```

若是有多个分支，就要写“清楚”点了，不管你当前在哪个分支上：

```bash
git push origin master
git push origin 分支名
```

直接 `git push` ，Git 会报错，并提示一个参考性的命令操作：

```bash

```

所以请一定“清楚”描述你的指令，不要让 Git 来猜测你想干嘛！

在使用 `git push` 系列命令之前，请确定你至少按如下顺序执行了这两类 git 命令：

```bash
git add
git commit
```

## 当你 fork 了一个项目仓库后

假如你想为这个项目贡献代码，且还有其他人在同时为这仓库贡献代码时，你或许（其实是一定）需要做下面的事情，为后续的 Coding 提供一些方便。

因为你会遇到如下的“困扰”/不了解：

1. 在你 fork 之后，原仓库又更新（有了新的 commit ）
2. 且 GitHub 并不会贴心地为你将这些原仓库的更新自动 “同步” 到你 fork 的仓库下
3. 若不在你提 Pull Request 前，同步下原仓库的更新到你的 fork 仓库，GitHub （可能）会提示错误（为什么说是“可能”呢，因为我没亲自试过这样的“错误”操作。为了安全起见还是尽量先同步再 Pull Request 吧，哈哈哈哈）。

### 查看当前本地仓库的远程仓库路径/链接

如题操作的命令如下

```bash
git remote -v
```

你将看到

```bash
origin 你的远程仓库链接 (fetch)
origin 你的远程仓库链接 (push)
```

接着

### 添加“上游”仓库远程链接

```bash
git remote add upstream 原仓库链接
```

这里的 `upstream` ，是“上游”的意思。你可以根据你的习惯/想法来定义这个名字叫啥。

此外，建议你使用的原仓库链接类型（HTTPS or SSH），跟你的 fork 仓库所绑定到本地的链接类型一致。因为我在实际操作中，曾遇到：在我使用 SSH 作为 fork 仓库的链接，但原仓库使用的是 HTTPS 后拉取原仓库到本地时，Git 就报错。

当时的报错如下：

```bash
efrror: RPC failed; curl 56 OpenSSL SSL_read: SSL_ERROR_SYSCALL, errno 10054
atal: the remote end hung up unexpectedly
fatal: protocol error: bad pack header
```

但删掉这个 HTTPS 类型链接后，添加 SSH 类型链接，再拉取就不会报错了。

顺便说下,如何删除远程仓库链接：

```bash
git remote rm 远程名称
```

但在网上查询相关，又发现（可能）是因为 HTTPS 的 SSL 验证的问题，他们的解决方案如下：

```bash
git config --global http.sslVerify false
```

## 分支 branch

### 查看分支

- 查看 **本地** 分支

  ```bash
  git branch -a
  ```

- 查看 **远程** 分支

  ```bash
  git branch -a
  ```

- 查看所有本地分支及当前的所有远程本地关联情况

  ```bash
  git branch -a
  ```


### 新建本地分支

- 只是单纯的新建，并不切换到新建的本地分支上

  ```bash
  git branch <branch-name>
  ```

  - 创建新的本地分支并立刻切换过去

    ```bash
    git checkout -b <branch-name>
    ```

### 删除分支

- 在本地
  - 删除已参与合并的本地某分支

    ```bash
    git branch -d <branch-name>
    ```

    `-d`：**只能删除已参与了合并的分支**，对未有合并的分支无法删除。

  - 强制删除本地某分支

    ```bash
    git branch -D <branch-name>
    ```

    `-D`：强制删除！

- 在远程

  - 可在 Web 上进行图形化操作。GitHub 上是在 *View all branches* 页面（链接大概就是：仓库地址+'branches'）

    假如你是先在远程删除了分支，那么你需要以如下方式来同步到本地

    - 我们先来查看下远程和本地分支情况：

        ```bash
        git remote show origin
        ```

        若有差异，会显示如下类似内容：

        ```bash
        ***************
        Remote branches:
        Vue2.x                    tracked
        master                    tracked
        refs/remotes/origin/test  stale (use 'git remote prune' to remove) #1
        refs/remotes/origin/test1 stale (use 'git remote prune' to remove) #2
        ***************
        ```

        #1 和 #2 的分支，便是在远程已删除的分支。

    - 假如你想同步远程分支的变化到本地：
      - 先删除本地分支的无效关联

        ```bash
        git remote prune origin
        ```

        注意：这个命令 **只是移除远程已删除分支跟本地对应分支之间的关联/链接。**

        在执行后，被移除与远程对应分支关联/链接的本地分支并没有被删除。可以通过 `git branch` / `git branch -a` 进行查询验证。

        在这里，`git pull`，并不能用来同步分支变更）

      - 再 **手动** 强制删除本地分支

        ```bash
        git branch -d <branch-name>
        ```

        是的！你没看错！目前只找到手动的方法去一一删除。因为虽然有找到一个通过过滤来删除无用分支的方法，但命令有点复杂不方便记忆和理解，索性还是手动一一删除的好。

  - 也可在本地删除远程的分支：

    ```bash
    git push origin :heads/<branch-name>
    ```

    该方式还删除了该分支远程和本地的关联，但本地的对应分支还是在的。还是得手动删除对应本地分支。

### 合并分支

```bash
git merge <branch-name>
```

**注意**：这是将 `<branch-name>` 与当前分支（比如当前在 master 上）合并。

### 将本地分支同步到远程


```bash
git push origin <branch-name>:<branch-name>
```

上传本地的 test 分支作为远程的 test 分支

```bash
git push origin test:test
```

以上才是同步本地分支到远程的正确姿势！

**切记不要像下面这般**，虽然也可以同步，但会自动触发远程仓库的预合并到 master！虽然可以关闭，但仍很麻烦！

```bash
git push
# or
git push origin test
```

###