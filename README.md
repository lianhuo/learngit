## GitNotes
[廖雪峰老师的Git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

### 创建版本库
初始化一个Git仓库，使用 `git init` 命令  
添加文件到Git仓库，分两步：
  * 第一步，使用命令`git add <file>`，注意，可反复多次使用，添加多个文件；
  * 第二步，使用命令`git commit`，完成,注意添加 -m 消息

### 时光机穿梭
`git status` 命令可以让我们时刻掌握仓库当前的状态,虽然Git告诉我们readme.txt被修改了，但如果能看看具体修改了什么内容，需要用`git diff`这个命令看看
 * 要随时掌握工作区的状态，使用`git status`命令。
 * 如果git status告诉你有文件被修改过，用`git diff`可以查看修改内容。

### 版本回退
`git log`命令显示从最近到最远的提交日志，如果嫌输出信息太多，看得眼花缭乱的，可以试试加上`--pretty=oneline`参数。  
在Git中，用`HEAD`表示当前版本，上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个^比较容易数不过来，所以写成`HEAD~100`。
  * `HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。
  * 用`git log`可以查看提交历史，以便确定要回退到哪个版本。
  * 用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。

### 撤销修改
`git checkout -- file`可以丢弃工作区的修改
  * 想直接丢弃工作区的修改时，用命令`git checkout -- file`。
  * 改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD file`，第二步用`git checkout -- file`。
  * 已经提交了不合适的修改到版本库时，想要撤销本次提交,可以使用版本回退

### 删除文件
命令`git rm`用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。

### 添加远程库
* 要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`；
* 关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；
* 此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；

### 从远处库克隆
 * 要克隆一个仓库，首先必须知道仓库的地址，然后使用`git clone`命令克隆。
 `git clone git@github.com:项目.git`
 * Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。

### 创建与合并分支

* 查看分支：`git branch`
* 创建分支：`git branch <name>`
* 切换分支：`git checkout <name>`
* 创建+切换分支：`git checkout -b <name>`
* 合并某分支到当前分支：`git merge <name>`
* 删除分支：`git branch -d <name>`

### 解决冲突
* 当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
* 用`git log --graph`命令可以看到分支合并图。

### 分支管理策略
合并分支时，Git会用`Fast forward`模式，但这种模式下，删除分支后，会丢掉分支信息。
如果要强制禁用`Fast forward`模式，Git就会在`merge`时生成一个新的`commit`，这样，从分支历史上就可以看出分支信息。
 * 合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。

### Bug分支
Git提供了一个`stash`功能，可以把当前工作现场“储藏”起来，用`git stash list`命令查看储藏的工作区，恢复工作区：一是用`git stash apply`恢复，但是恢复后，`stash`内容并不删除，你需要用`git stash drop`来删除；
另一种方式是用`git stash pop`，恢复的同时把stash内容也删了
* 当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场。

### Feature分支
 * 开发一个新feature，最好新建一个分支；
 * 如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`强行删除。

### 多人协作　
当你从远程仓库克隆时，实际上Git自动把本地的`master`分支和远程的`master`分支对应起来了，并且，远程仓库的默认名称是`origin`。
要查看远程库的信息，用`git remote`,或者，用`git remote -v`显示更详细的信息;  
多人协作的工作模式通常是这样：
    * 首先，可以试图用`git push origin branch-name`推送自己的修改
    * 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
    * 如果合并有冲突，则解决冲突，并在本地提交；
    * 没有冲突或者解决掉冲突后，再用`git push origin branch-name`推送就能成功！
    * 如果`git pull`提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream branch-name origin/branch-name`。
小结：
  * 查看远程库信息，使用`git remote -v`；
  * 本地新建的分支如果不推送到远程，对其他人就是不可见的；
  * 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；
  * 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
  * 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
  * 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。
