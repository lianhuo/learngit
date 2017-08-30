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
