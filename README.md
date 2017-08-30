## GitNotes

### 创建版本库

初始化一个Git仓库，使用 `git init` 命令  
添加文件到Git仓库，分两步：
  * 第一步，使用命令`git add <file>`，注意，可反复多次使用，添加多个文件；
  * 第二步，使用命令`git commit`，完成,注意添加 -m 消息

### 时光机穿梭

`git status` 命令可以让我们时刻掌握仓库当前的状态,虽然Git告诉我们readme.txt被修改了，但如果能看看具体修改了什么内容，需要用`git diff`这个命令看看
 * 要随时掌握工作区的状态，使用`git status`命令。
 * 如果git status告诉你有文件被修改过，用`git diff`可以查看修改内容。
#### 版本回退
`git log`命令显示从最近到最远的提交日志，如果嫌输出信息太多，看得眼花缭乱的，可以试试加上``--pretty=oneline`参数 
