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
* git switch (branch) 切换到分支
* git switch -b (branch-name)
* git branch 查看所有分支
* git branch -d (branch-name)删除分支
* git merge (branch-name) 将分支合并到当前分支
## GitHub笔记
### 复制GitHub项目到本地
* git clone (repository-url) 克隆仓库到本地
### Git remote
* git remote add orgin (repository-url) or (repositor-ssh_keys)添加远程仓库
* git remote -v 查看与本地仓库关联的远程仓库
### Git push
* git push origin master 推送到远程仓库默认的master分支
* git push -u origin master 默认推送至origin master 以后直接git push即可 -u：这个选项会将本地的 master 分支与远程的 origin/master 分支关联。当你使用 git push 或 git pull 命令时，Git 会默认使用这个关联的远程分支。