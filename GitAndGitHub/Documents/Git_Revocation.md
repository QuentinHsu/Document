# Git Revocation

Git 撤销

> 参考资料：
> [使用Git，10件你可能需要“反悔”的事 · DevUI 团队](https://segmentfault.com/a/1190000022951517)

## 1. 未暂存前，撤销本地更改：`checkout`

在没有暂存（git add）之前，查看本地更改：

```bash
git diff
```

撤销 **当前 所有 未暂存 的更改**

```bash
git checkout -- .
```

**不可反悔**，不可 “ **撤销** ” 刚刚的 “ **撤销** ”。

撤销 **指定文件** 的更改

```bash
git checkout -- <fileName>
```
## 2. 已暂存后，撤销暂存区的更改：`reset`

查看暂存区的更改

```bash
git diff --staged
```

撤销 **当前 所有 已暂存 文件的更改**

```bash
git reset .
```

撤销 **当前 指定 已暂存 文件的更改**

```bash
git reset <fileName>
```

## 撤销 **未提交的所有更改**

合并 1 和 2 的命令

```bash
git reset --hard
```

等效于

```bash
git reset .
git checkout --
```

## 3. 撤销未推送到远程仓库的本地提交

假定将被撤销的提交 Commit ID 为 `819cff0`，它的上一次 Commit ID 为 `ecbff77`

另外，查看本地提交记录：

```bash
git log
```

- 方法1： **checkout**

    **明确** 回到上一次提交 `ecbff77`

    ```bash
    git checkout ecbff77
    ```

- 方法2： **reset** 重置

    重置之前的 1 次提交

    ```bash
    git reset --hard HEAD~1
    ```

    重置之前的 n 次(最新的 1 次到往之前数的第 n 次)提交

    ```bash
    git reset --hard HEAD~n
    ```

    **可反悔**，操作步骤如下：

        1. 找到被重置的提交，发现是 `819cff0`

            ```bash
            git reflog
            ```

        2. 使用 reset 回到该提交

            ```bash
            git reset --hard 819cff0
            ```
    感觉 reset 更像是隐藏/注释了提交，并不是完全删除了。

## 4. 修改提交: `--amend`

`--amend`，会修改掉原始的 Commit ID，生成新的 Commit ID。并不会生成新的一个提交。

### 提交遗漏的文件

步骤：
1. 暂存遗漏的文件
2. **追加** 进当前最新的提交记录中

    ```bash
    git add <file>
    git commit --amend
    ```

### 修改提交信息

- 直接在命令行中修改提交信息

    ```bash
    git commit --amend -m "new commit message"
    ```

- 在特定的页面(例如： VS Code)中修改提交信息

    ```bash
    git commit --amend
    ```

    执行该代码后，弹出特定的修改操作页面。

## 5. 撤销特定的某一次提交：`revert`

假定将被撤销的提交 Commit ID 为 `819cff0`，该提交位于提交历史比较早期的位置。

```bash
git revert 819cff0
```

该命令 **只是撤销指定提交的更改内容，并不会删除该提交记录。**
**并会生成一个新的提交记录，以记录该撤销操作。**

## 6. 撤销出现冲突的合并操作

```bash
git merge --abort
```

假如是 VS Code 作为开发编辑工具，推荐使用 [GitLens — Git supercharged](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens) 插件来处理冲突。十分的直观和可视化地显示冲突情况。

## 暂存区/分支上的文件，想“移除”

- 假如 “移除”，是完全删除

    ```bash
    git rm <file path>
    ```

- 假如 “移除”，只是取消暂存/版本管理

    ```bash
    git rm --cathed <file path>
    ```

## 8. 分支重命名

```bash
git br -m [old_br] [new_br]
```

## 9. 撤销变基操作

### 什么是变基？

详情请见：[3.6 Git 分支 - 变基 · Git-SCM](https://git-scm.com/book/zh/v2/Git-分支-变基)

将 rebase_test 分支的修改变基到 master 上：

```bash
git checkout rebase_test
git rebase master
```

撤销步骤：

1. 使用 git reflog 命令找到 **变基前** 的提交 09b0adc
2. 使用 git reset --hard 09b0adc 重置到该提交

## 10. 以脚本方式改写提交

### 彻底移除提交历史的某一文件

考虑以下场景，在一次很早的提交中，将一个储存密码的文件 passwords.txt 提交到了远程仓库，这时如果只是从远程仓库中删除该文件，别人依然可以通过提交历史找到这个文件。

因此我们需要从每一个快照中移除该文件：

```bash
git filter-branch --tree-filter 'rm -f passwords.txt' HEAD
```
该命令执行完会将提交历史中所有提交的 passwords.txt 文件彻底删除，永远没法通过 Git 找回。