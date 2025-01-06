# Git 和 Git hub 笔记
## Git笔记
### Git的配置
#### 三个不同的配置级别
* system 代表所有用户
* global 代表当前用户的所有存储库
* local 代表当前用户的当前存储库
#### git用户的配置
* git config --global user.name "Brain" 设置用户名
* git config --global user.email "2510668237@qq.com" 设置邮箱
* git config --global core.editor "code --wait" 设置等待直到关闭vs code
* git config --global -e 打开所有全局设置
* git config --global core.autocrlf true 当你在 Windows 上工作时，设置为 true 将自动将 LF（Unix 换行符）转换为 CRLF（Windows 换行符）在检出时；而在提交时，会将 CRLF 转换回 LF。这有助于避免在不同操作系统间共享代码时出现换行符不一致的问题。
### Git的帮助
* git -h 获取帮助
### Git的初始化
* git init 表示在项目中初始化一个git存储库
    * ls -a 显示出隐藏目录 -a代表显示所有
    * ls -la 显示出所有隐藏目录 -l 代表显示长格式，显示更详细的信息
    * rm -rf 代表删除所有并且不提示 -r 代表递归 -f 代表强制删除
### Git的暂存文件
* echo hello >file1.txt 这里>代表覆盖并写入，>>代表在文件后面写入
* git status 代表git暂存区域的状态
* git status 代表git暂存区域状态的简略版
* git add 把文件加入到暂存区域中
  * git add . 代表加入所有文件
  * git add *.txt 代表加入所有同样后缀的文件
### Git的提交
* git commit -m "message" 将文件从暂存区域中提交到本地仓库并且附带提交信息 
### Git的直接提交(跳过暂存)
* git commit -am "message" -a 代表所有
### Git的删除文件
* rm (filename)仅仅是Linux命令，还需要添加到暂存区域和提交到本地仓库
* git rm (filename) 省去了添加和提交，直接删除
### Git的重命名或移动文件
* mv (filename1) (filename2) 仅仅是Linux命令，还需要添加到暂存区域和提交到本地仓库
* git mv (filename1) (filename2) 省去了添加和提交，直接重命名
### Git ignore
### Git中比较差异
* git diff 显示工作目录但是未暂存的差异
* git diff --staged 显示暂存区的更改
* git diff (filename) 显示指定文件的更改
* git diff (branchname) 显示当前分支与指定分支的差异
### Git检查提交历史
* git log 检查提交历史
  * git log --oneline 提交历史的简略版
### Git检查提交的具体更改
* git show (commitid) 检查具体提交的更改
    * git show HEAD~1 HEAD代表头指针，1代表从头指针往下数第1个
### Git中撤销的操作
* git restore (filename) 恢复未暂存的更改
* git restore --staged (filename) 恢复已暂存的更改，恢复到未暂存状态
* git restore --source=(commitid) (filename) 特定提交中恢复文件
### Git中分支的操作
* git branch (branch-name) 创建分支
* ***git switch (branch) 切换到分支***
* git switch -b (branch-name)
* git branch 查看所有分支
* git branch -d (branch-name)删除分支
* git merge (branch-name) 将分支合并到当前分支
## GitHub笔记
### 复制GitHub项目到本地
* git clone (repository-url) 克隆仓库到本地
### Git remote
* ***git remote add orgin (repository-url) or (repositor-ssh_keys)添加远程仓库***
* git remote -v 查看与本地仓库关联的远程仓库
### Git push
* git push origin master 推送到远程仓库默认的master分支
* git push -u origin master 默认推送至origin master 以后直接git push即可 -u：这个选项会将本地的 master 分支与远程的 origin/master 分支关联。当你使用 git push 或 git pull 命令时，Git 会默认使用这个关联的远程分支。
### Git fetch
* git fetch 拉取远程更新，但不直接合并
### Git fork
目的: 创建一个你自己拥有的远程仓库副本，通常用于开源项目贡献。当你 fork 一个项目时，你实际上复制了原始仓库的内容，但你对 fork 出来的仓库拥有完全的控制权限。

适用场景: 你想对一个开源项目进行贡献时，首先将该项目 fork 到你自己的账户下，然后克隆到本地进行开发，最后通过 Pull Request 提交代码到原仓库。
## Git tag
标签常用于标记一个特定的点(通常是某个版本发布点),让开发者可以方便地引用和定位到那个特定的提交.
1. 创建标签
   1. 创建轻量标签
      轻量标签就是简单地指向某个提交，不带任何附加信息。
      ```shell
      git tag <tag_name>
      ```
      例如：
      ```shell
      git tag v1.0
      ```
   2. 创建附注标签(Annotated Tag)

      附注标签包含了创建者、日期、注释以及可能的签名。
      ```shell
      git tag -a <tag_name> -m "Tag message"
      ```
      例如：
      ```shell
      git tag -a v1.0 -m "First release"
      ```
   3. 给特定的提交创建标签
  
      可以指定一个提交哈希值来给该提交打标签：
      ```shell
        git tag <tag_name> <commit_hash>
      ```
        例如：
      ```shell
      git tag v1.0 1a2b3c4d
      ```
2. 查看标签
    ```shell
    git tag
    ```
    这会列出当前仓库中的所有标签。

    要查看某个特定标签的信息，可以使用：
    ```shell
    git show <tag_name>
    ```
    例如：
    ```shell
    git show v1.0
    ```
3. 删除标签

    要删除本地标签：
    ```shell
    git tag -d <tag_name>
    ```
    例如：
    ```shell
    git tag -d v1.0
    ```
4. 推送标签到远程仓库

    默认情况下，git push 不会推送标签。需要显式推送：

    推送单个标签：
    ```shell
    git push origin v1.0.0
    ```
    推送所有标签：
    ```shell
    git push origin --tags
    ```
## Git stash
在 Git 中,<kbd>git stash</kbd>是一个非常有用的命令，用于临时保存当前工作目录和暂存区的改动，以便可以切换到其他分支或进行其他操作，而不需要提交这些更改。它允许你在不提交当前工作进度的情况下，将这些更改保存到一个堆栈中，稍后可以恢复。

* git stash 的常见用途：

  * 切换分支：你正在开发一个特性，但突然需要切换到其他分支来修复 bug 或查看其他内容。你不希望提交当前的工作，但又不想丢失正在进行的更改，使用 git stash 可以临时保存这些更改。
  * 中断工作：当你还没有准备好提交时，你可以使用 stash 来临时保存你的工作进度，以便稍后恢复。
  * 清理工作区：在某些情况下，你需要一个干净的工作目录来进行测试或其他操作，可以使用 git stash 来暂时清理当前的更改。
* 常用操作

1. 保存当前修改

     1. 保存工作目录和暂存区的修改：
      ```shell
      git stash
      ```
      默认保存的 stash 会命名为 <kbd>stash@{0}</kbd>。

     2. 保存并添加描述信息：
      ```shell
      git stash save "描述信息"
      ```

     3. 保存未跟踪的文件（新增的文件）：
      ```shell
      git stash -u
      ```

2. 查看保存的 stash 列表
      ```shell
      git stash list
      ```
3. 恢复最新的 stash 并删除 stash 记录
    ```shell
    git stash pop
    ```
    不删除stash
    ```shell
    git stash apply
    ```
## Git rebase
Rebase(变基):将当前分支的提交“移动”到目标分支的最新提交之后，形成一条直线历史。
与 merge 的区别：

   * <kbd>merge</kbd>会创建一个新的合并提交，保留分支的历史。

   * <kbd>rebase</kbd>则不会创建合并提交，而是将提交重新应用到目标分支上，形成线性历史。
常见的用法：

   1. 将当前分支的修改重新应用到另一个分支的顶部：
      ```shell
      git checkout feature-branch  # 切换到需要进行 rebase 的分支
      git rebase main  # 将当前分支的修改应用到 main 分支的顶部
      ```
   2. 交互式 rebase： 你可以使用 -i 选项进行交互式的 rebase，以便在 rebase 过程中修改提交历史。
      ```shell
      git rebase -i HEAD~5  # 交互式 rebase，修改最近 5 次提交
      ```
   3. 解决冲突： 在 rebase 过程中，如果发生冲突，Git 会暂停，并提示你解决冲突。解决冲突后，需要运行以下命令继续 rebase：
      ```shell
      git add <file>  # 标记冲突已解决
      git rebase --continue  # 继续 rebase
      ```
   4. 放弃 rebase 操作： 如果在 rebase 过程中遇到问题，或者想要放弃 rebase，可以使用以下命令：
      ```shell
      git rebase --abort  # 放弃当前的 rebase 操作，恢复到原来的状态
      ```
使用场景：

  * 清理历史：当你有一个长时间进行开发的分支，期间与主分支有很多不同步的提交，通过<kbd>rebase</kbd>可以将这些提交整理得更清晰。
  * 避免重复的合并提交：如果多个开发者在不同的分支上进行开发,<kbd>rebase</kbd>可以帮助减少冗余的合并提交，保持历史记录的整洁。

注意事项：

  * 重写历史:<kbd>rebase</kbd>会重写提交历史，因此它最好只在自己本地分支上使用，如果其他人也在使用该分支，使用 rebase 可能会导致问题。
  * 避免在公共分支上使用：如果分支已经被推送到远程并被其他开发者拉取，最好不要使用<kbd>rebase</kbd>，因为这会改变历史，导致其他开发者的仓库与远程仓库不同步。
## Git cherry-pick
git cherry-pick 是 Git 中的一个命令,用于将某个提交(或多个提交)从一个分支应用到当前分支.这使得你能够选择性地将其他分支上的某些提交复制到当前分支,而不是合并整个分支或者使用 rebase。
语法：
  ```shell
  git cherry-pick <commit-hash>
  ```
其中 <commit-hash> 是你想要挑选的提交的哈希值。

示例：

假设你在 feature 分支上有如下提交历史：
```shell
A---B---C---D  (feature)
```
你想把提交<kbd>B</kbd>和<kbd>D</kbd>从 feature 分支应用到<kbd>main</kbd>分支上。

1. 首先，切换到 main 分支：
```shell
git checkout main
```
2. 然后，使用 cherry-pick 将 feature 分支上的 B 和 D 提交应用到 main 分支上：
```shell
git cherry-pick <commit-hash-of-B>
git cherry-pick <commit-hash-of-D>
```
每个提交都会被单独应用到当前分支（main），并生成新的提交。

结果是 main 分支会有类似下面的提交历史：
```shell
    A---B---C---D  (feature)
                \
                 B'---D'  (main)
```
其中<kbd>B'</kbd>和<kbd>D'</kbd>是原始提交<kbd>B 和</kbd>D的拷贝,哈希值不同,但内容相同。

常见选项：

1. 多个提交： 你可以一次性挑选多个连续的提交：
```shell
git cherry-pick <commit-hash1>^..<commit-hash2>
```
这会将从 <commit-hash1> 到 <commit-hash2> 之间的所有提交挑选到当前分支。

2. 解决冲突： 在 cherry-pick 的过程中，如果发生冲突，Git 会暂停并提示你解决冲突。你需要手动解决冲突，然后使用以下命令继续操作：
```shell
git add <resolved-file>
git cherry-pick --continue
```
3. 跳过提交： 如果你决定跳过某个有冲突的提交，可以使用：
```shell
git cherry-pick --skip
```
这会跳过当前有冲突的提交，并继续应用下一个提交。

4. 放弃 cherry-pick 操作： 如果你在过程中决定放弃 cherry-pick，可以使用：
```shell
git cherry-pick --abort
```
这会取消当前的 cherry-pick 操作，恢复到操作之前的状态。
## Git flow
1. windows版本git自带git flow,检查是否安装git flow
    ```shell
    git flow version
    ```
### Git Flow 分支模型

master 分支：

  * 永远保持稳定和可发布的状态。
  * 每次发布一个新的版本时，都会从 develop 分支合并到 master 分支。

develop 分支：

  * 用于集成所有的开发分支。
  * 代表了最新的开发进度。
  * 功能分支、发布分支和修复分支都从这里分支出去，最终合并回这里。

feature 分支：

  * 用于开发新功能。
  * 从 develop 分支创建，开发完成后合并回 develop 分支。
  * 命名规范：feature/feature-name。

release 分支：

  * 用于准备新版本的发布。
  * 从 develop 分支创建，进行最后的测试和修复，然后合并回 develop 和 master 分支，并打上版本标签。
  * 命名规范：release/release-name。

hotfix 分支：

  * 用于修复紧急问题。
  * 从 master 分支创建，修复完成后合并回 master 和 develop 分支，并打上版本标签。
  * 命名规范：hotfix/hotfix-name。

![git_flow_interface](https://www.runoob.com/wp-content/uploads/2024/07/git-flow.png)
### Git flow 工作流程
1. 初始化 Git Flow

首先，在项目中初始化 Git Flow。可以使用 Git Flow 插件（例如 git-flow）来简化操作。
```shell
git flow init
```
初始化时，你需要设置分支命名规则和默认分支。
2. 创建功能分支

当开始开发一个新功能时，从 develop 分支创建一个功能分支。
```shell
git flow feature start feature-name
```
完成开发后，将功能分支合并回 develop 分支，并删除功能分支。
```shell
git flow feature finish feature-name
```
3. 创建发布分支

当准备发布一个新版本时，从 develop 分支创建一个发布分支。
```shell
git flow release start release-name
```
在发布分支上进行最后的测试和修复，准备好发布后，将发布分支合并回 develop 和 master 分支，并打上版本标签。
```shell
git flow release finish release-name
```
4. 创建修复分支

当发现需要紧急修复的问题时，从 master 分支创建一个修复分支。
```shell
git flow hotfix start hotfix-name
```
修复完成后，将修复分支合并回 master 和 develop 分支，并打上版本标签。
```shell
git flow hotfix finish hotfix-name
```
实例操作

以下是一个实际使用 Git Flow 的综合实例。

初始化 Git Flow：
```shell
git flow init
```
创建和完成功能分支：
```shell
git flow feature start new-feature # 开发新功能
git flow feature finish new-feature
```
创建和完成发布分支：
```shell
git flow release start v1.0.0 # 测试和修复
git flow release finish v1.0.0
```
创建和完成修复分支：
```shell
git flow hotfix start hotfix-1.0.1. # 修复紧急问题
git flow hotfix finish hotfix-1.0.1
```