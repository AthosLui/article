# Git 只言片语

[link](http://gitref.org/zh/basic)

### git clone

`git clone url` 检出代码到本地，以项目名新建文件夹  
`git clone <url> [FolderName]` 自定义文件夹名

### git add

添加文件到缓存区，可以接多个文件名，以空格分开  
`git add .`：添加所有修改  
`git add *`：添加当前目录所有修改

### git diff

退出快捷键：`q`  
`git diff` 列出未上次提交快照之后尚未缓存的所有更改  
`git diff --cached` 已经写入缓存的改动  
`git diff HEAD` 显示**所有**的改动

### git status

查看当前修改状态，`git status -s` 为输入简洁版  
文件左边为红色表示没有追踪，绿色反之

### git commit

将 `add` 的缓存文件记录快照  
`git commit --amend`：修改提提交信息  
`git commit -a` 对所有有提交记录的文件执行`git add`，所以不会执行新增文件  
提交已经追踪的代码（status 左边为绿色的）

### git reset HEAD

取消缓存已缓存的内容  
`git reset HEAD -- <fileName>` 取消默认文件的缓存

### git checkout

`git checkout <branchname>` 切换分支  
`git checkout -b <branchname>` 先创建分支，再切换到该分支  

### git branch

`git branch` 列出本地分支  
`git branch -r` 列出远端分支  
`git branch -a` 列出所有分支  
`git branch -d <branchname>` 删除分支『前提是目前分支不在此分支』

### git log

`git log` 显示一个分支中提交的更改记录  
`git log --oneline` 选项来查看历史记录的紧凑简洁的版本  
`git log --graph` 选项来查看历史记录的拓扑图

### git remote

`git remote` 列出远端别名
`git remote -v` 列出远端别名，并且可以看到每个别名的实际链接地址