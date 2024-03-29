# Git

## Git的作用？

Git可以在同一个目录中保存N个版本，可以切换以前的版本，方便地查看以前的修改记录。

允许建立多个分支，可以根据不同需求在某个版本的基础上建立新的分支，用于多人协作。

##  Git是分布式还是集中式？

Git是一种分布式版本控制系统。

## 初始化仓库命令是什么？

git init

## 工作区域有哪几个？文件状态有哪几种？

Git本地有四个工作区域：工作区、暂存区、版本库、远程仓库。

工作区：平时存放项目代码的地方。

暂存区：用于临时存放改动的地方，是一个文件，保存即将提交到文件列表信息。

版本库：安全存放数据的位置，这里面有提交到所有版本的数据。其中HEAD指向最新放入仓库的版本。

远程仓库：托管代码的服务器。

文件状态

新建文件—>Untracked

使用git add命令将新建的文件加入到暂存区—>Staged

使用commit命令将暂存区的文件提交到本地仓库—>Unmodified

如果对Unmodified状态的文件进行修改—> modified

如果对Unmodified状态的文件进行remove操作—>Untracked

Untracked: 未跟踪, 此文件在文件夹中, 但并没有加入到git库, 不参与版本控制. 通过`git add` 状态变为`Staged`.

Unmodify: 文件已经入库, 未修改, 即版本库中的文件快照内容与文件夹中完全一致. 这种类型的文件有两种去处, 如果它被修改, 而变为`Modified`. 如果使用`git rm`移出版本库, 则成为`Untracked`文件

Modified: 文件已修改, 仅仅是修改, 并没有进行其他的操作. 这个文件也有两个去处, 通过`git add`可进入暂存`staged`状态, 使用`git checkout` 则丢弃修改过, 返回到`unmodify`状态, 这个`git checkout`即从库中取出文件, 覆盖当前修改

Staged: 暂存状态. 执行`git commit`则将修改同步到库中, 这时库中的文件和本地文件又变为一致, 文件为`Unmodify`状态. 执行`git reset HEAD filename`取消暂存, 文件状态为`Modified`

## 添加追踪命令是什么？提交命令是什么？

**添加追踪命令：**

git add 文件名	单个文件

git add .				所有文件

**提交命令：**

git commit -m "提示语"

## 版本回退命令是什么？有哪些可选参数？有哪几种回退方式？

在 Git 中，版本回退的命令是 `git reset`。`git reset` 命令用于移动 HEAD 指针和当前分支引用来指向指定的提交，从而实现版本回退。`git reset` 命令的常用参数和回退方式如下：

可选参数：
1. `--soft`：仅仅将 HEAD 指向的提交回退到指定的提交，暂存区和工作目录中的文件保持不变。
2. `--mixed`（默认）：将 HEAD 指向的提交回退到指定的提交，暂存区的文件会被重置为指定提交的状态，但工作目录中的文件不受影响，需要重新提交。
3. `--hard`：彻底回退到指定的提交，HEAD 指针、暂存区和工作目录都会被重置为指定提交的状态，之后的修改全部丢失。

回退方式：
1. 回退到指定的提交：通过指定提交 ID 或引用（如分支名、tag 等）来将 HEAD 指针回退到特定的提交，从而回退到该版本的状态。
2. 回退到相对位置：使用 `HEAD~<num>` 表示相对当前提交向前的偏移量，例如 `git reset --hard HEAD~2` 表示将 HEAD 回退两个提交。
3. 回退到某个分支/标签：通过指定分支名或标签名来将当前分支回退到该分支/标签指向的提交。

在使用 `git reset` 进行版本回退时，请谨慎操作，确保你理解回退的影响，并在必要时备份重要数据。

## gitignore忽略文件怎么写？分别查询一下你们所用语言/框架一般会忽略提交哪些文件？

文件和文件夹的忽略规则：

在 `.gitignore` 文件中，每行写入一个规则。可以使用通配符、路径和模式匹配来指定需要忽略的文件和文件夹。常见的规则示例：

- 忽略单个文件：

     ```
     filename.ext
     ```

- 忽略特定文件类型（如日志、编译生成的文件等）：

     ```
     *.log
     *.exe
     ```

- 忽略指定文件夹：

     ```
     folder/
     ```

- 忽略特定路径下的文件：

     ```
     path/to/file
     ```

- 忽略特定路径中的所有文件和文件夹：

     ```
     path/*
     ```

注释：可以使用 `#` 符号作为注释，以便在 `.gitignore` 文件中添加注释说明。

忽略以下文件或文件夹：

- 编译生成的文件和文件夹（如 `.class`、`.jar`、`.dll`、`/bin/`、`/obj/` 等）。
- 临时文件和缓存文件（如 `*.tmp`、`*.cache`、`.DS_Store` 等）。
- 日志文件（如 `*.log`、`/logs/` 等）。
- 依赖管理工具生成的文件（如 `node_modules/`、`vendor/`、`.venv/` 等）。
- 配置文件中包含敏感信息的文件（如 `.env`、`.env.local`、`secrets.yml` 等）。
- 自动生成的文档文件（如 `/docs/`、`/site/` 等）。

## 仓库克隆命令是什么？如何关联本地仓库和远程仓库？

仓库克隆命令是 `git clone <远程仓库URL>`。

关联本地仓库和远程仓库的步骤如下：

1. 在本地创建一个新的 Git 仓库或进入已存在的 Git 仓库目录。
  
    ```
    mkdir my_project
    cd my_project
    ```

2. 关联远程仓库：将远程仓库的 URL 关联到本地 Git 仓库。
  
    ```
    git remote add origin <远程仓库URL>
    ```
   
    这里的 `origin` 是远程仓库的别名，你可以自定义，一般情况下使用 `origin`。

3. 拉取远程仓库内容并将远程主机的内容拉取到本地：使用 `git pull <远程主机名> <远程分支名>:<本地分支名>` 命令获取远程仓库的更新内容到本地仓库。
  
    ```
    git pull origin main:main
    ```

4. 推送本地修改到远程仓库：使用 `git push <远程主机名> <本地分支名>:<远程分支名>` 命令将本地修改推送到远程仓库。
  
    ```
    git push origin main:main
    ```

## 分支操作基本命令有哪些？

1. 查看所有分支：
   ```
   git branch
   ```

2. 创建新分支：
   ```
   git branch <branch_name>
   ```

3. 切换到指定分支：
   ```
   git checkout <branch_name>
   ```

4. 创建新分支并立即切换到该分支：
   ```
   git checkout -b <branch_name>
   ```

5. 合并指定分支到当前分支：
   ```
   git merge <branch_name>
   ```

6. 删除分支：
   ```
   git branch -d <branch_name>
   ```

7. 强制删除分支，即使有未合并的修改：
   ```
   git branch -D <branch_name>
   ```

8. 将本地分支推送到远程仓库：
   ```
   git push <remote_name> <branch_name>
   ```

9. 拉取远程分支到本地：
   ```
   git fetch <remote_name> <branch_name>
   ```

10. 将本地分支与远程分支关联：
    ```
    git branch --set-upstream-to=<remote_name>/<branch_name>
    ```

## 如何避免冲突？常用原则有哪些？

- `git status`查看冲突的文件
- 编辑器打开冲突的文件，查看冲突的内容

```text
未冲突的内容（两个分支都未改动）在分隔线外面
<<<<<<< HEAD
Git当前所在分支修改的内容（准确来说是HEAD指针指向的分支修改的内容）
=======
要合并过来的分支修改的内容
>>>>>>> branch_to_merge
```

- 怎样解决冲突？
  1. `git status`查看冲突的文件
  2. 编辑冲突文件，解决冲突（记得删除三行分隔线）
  3. `git add 冲突文件`
  4. `git commit -m "提交信息"`

## 如何进行版本回退和rebase？

**git reset**

git reset是一种比较暴力的版本回退方式回退到某个版本。

假设我们现在有一个代码库，其中有5个版本，我们想要回退到第3个版本。可以使用以下命令：

```cobol
git reset --hard HEAD~2
```

其中，HEAD表示当前版本，~2表示回退两个版本。执行完上述命令后，代码库中的版本就会回退到第3个版本。

假设我们现在有一个代码库，其中有5个版本，我们想要回退到某个提交ID为123456的版本。可以使用以下命令：

```cobol
git reset --hard 123456
```

执行完上述命令后，代码库中的版本就会回退到提交ID为123456的版本。

如果想要将更改推送到远程仓库，您需要使用 `git push` 命令来将更改推送到远程仓库。但是，由于 `git reset` 命令会更改本地分支的历史记录，因此您需要使用 `git push` 命令的 `-f` 或 `--force` 选项来强制推送更改，这将覆盖远程仓库中的历史记录、

以下是将更改推送到远程仓库的步骤：

使用 `git reset` 命令撤销本地提交。例如，如果您要撤销最新的提交并将更改还原到上一个提交，则可以使用以下命令：

```cobol
git reset HEAD~1
```

```perl
git push -f origin master
```

注意，`-f` 或 `--force` 选项用于强制推送更改。如果您不使用此选项，则 `git push` 命令将失败，因为远程仓库中已经存在与本地分支不同的历史记录。

请注意，强制推送更改可能会导致其他人的工作丢失或冲突，因此请确保在使用此选项之前与团队成员进行沟通，并确保您知道自己在做什么。

**git revert**

git revert是一种比较温和的版本回退方式，它可以撤销某个提交的修改，同时保留该提交之后的修改。使用git revert命令时，需要指定要撤销的提交ID。

撤销某个提交的修改

假设我们现在有一个代码库，其中有5个版本，我们想要撤销第3个版本的修改。可以使用以下命令：

```cobol
git revert 123456
```

其中，123456表示要撤销的提交ID。执行完上述命令后，Git会自动创建一个新的提交，该提交会撤销第3个版本的修改，同时保留第3个版本之后的修改。

当您使用 `git revert` 命令撤销一个或多个提交时，Git会创建一个新的提交来撤销之前的更改。这意味着您可以像推送其他提交一样将撤销提交推送到远程仓库。

以下是将撤销提交推送到远程仓库的步骤：

使用 `git revert` 命令撤销一个或多个提交。例如，如果您要撤销最新的提交，则可以使用以下命令：

```undefined
git revert HEAD
```

这将创建一个新的提交，该提交包含了撤销之前提交所做的更改。

请注意，`git revert` 命令不会更改本地分支的历史记录，因此您不需要使用 `-f` 或 `--force` 选项来强制推送更改。但是，如果其他人在您之前推送了与您要撤销的提交相关的更改，则您可能需要解决冲突才能将新的撤销提交推送到远程仓库。

撤销多个提交的修改

假设我们现在有一个代码库，其中有5个版本，我们想要撤销第3个版本和第4个版本的修改。可以使用以下命令：

```cobol
git revert 123456 789012
```

其中，123456和789012表示要撤销的提交ID。执行完上述命令后，Git会自动创建两个新的提交，分别撤销第3个版本和第4个版本的修改，同时保留第4个版本之后的修改。

rebase 具体操作：

首先 master 拉取到最新版本，然后切换到 branch 分支，在branch分支执行 `git rebase master`，表示 branch 上新提交的 commit 节点会在 master 上的最新提交点后重新设立起点重新执行，若是有冲突则解决冲突，没有冲突执行 `git add`，然后执行 `git rebase --continue`，最后切换到 master 分支，执行 `git merge``master`。git merge 会将两个分支的最新提交点进行一次合并，形成一个新的提交点，最终形成树状的提交记录，如果觉得 merge 之后出现的分叉会难以管理，那么可以选择 rebase 操作来替代 merge。git rebase 操作是将要 rebase 的分支最新提交点作为新的基础点，将当前执行 git rebase master 的分支的新commit 点重新生成 commit hash 值，rebase 完后再次切换到另一条分支进行合并，就可以保证线性的 commit的记录。

