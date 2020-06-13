# 团队项目协作中的 Git 和 “远程 Git 仓库” 的使用

GitHub 只能使用官方提供的物理资源，但 GitLab 在能使用其官方提供的物理资源外，还可以私有部署。

所以（我认为）二者在使用上还是有一定的区别

## 实际案例

### 1. 在得知远程仓库已迁移时，但本地也已产生了新的代码更改

#### 场景

之前使用的远程仓库被迁移到新的仓库地址，但我已在本地产生了新的代码，且已上传到了旧的远程仓库。但我不想重新 clone 新的仓库，再去重新更改代码。

#### 解决方案：更改本地的远程链接地址

为保险起见，我们先检查本地的已有远程仓库链接

```bash
git remote -v
```

你将会看到类似于这样的信息

```bash
origin  url(fecth)
origin  url(push)
<shortName>  url2(fecth)
<shortName>  url2(push)
```

##### 步骤

- 删除本地现有的远程仓库链接

  ```bash
  git remote rm origin
  ```

  在执行这条命令之前，你可能会怀疑无法删除这个唯一的（默认）仓库链接，我当时也是的。可**实践证明：完全可以删除！请放心大胆的删除！**

- 添加新的远程仓库链接

  ```bash
  git remote add origin url
  ```

  在这里，我们依旧默认使用 **origin** 为本地仓库名。以避免不必要的麻烦。

  这时候，你再使用 **`git remote -v`** 查询本地的远程仓库链接，就会发现已经变成新的远程仓库链接了。

  **至此，本地仓库也完成了“迁移”。**

  若是此时在当前的远程仓库里，没有新的 commit ，你就可以直接 push 以上传你的本地代码更改了。

### 2. 仅拉取远程仓库的指定分支到本地

git clone 默认只会 clone master 分支上的内容

如需 clone 指定某分支：

```git
git clone -b <分支名> SSH/HTTPS
```

### 3. 强制 push 覆盖远程仓库内容

因为在本地的提交，不小心误删除了多个提交记录（在误删除前就已同步至远程）。

在本地修正了错误操作后，直接 push，是不可以的。因为远程和本地的提交记录有差异（本地缺失远程版本的某一个提交），继而会报如下错误。

```
> git push
To github.com:QuentinHsu/******.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'git@github.com:QuentinHsu/******.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

当确定是以本地仓库现有提交版本为最新的话，那我们就 **强制 push 覆盖远程仓库**

```
git push origin master --force
```

可能需要注意实际的分支情况