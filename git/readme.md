git是一款诞生于2005年的分布式版本控制工具。

首先说一下简单的git常用命令：  

git clone user@host:/path/project     #拷贝远程代码

一次简单完整的代码提交

git status     #查看状态
git add <file>     #建立跟踪
git commit     #完成提交
git push      #推送至远程服务器


我们常用的git命令还有：  

git pull #更新代码
git diff #查看修改了哪些内容，推荐每次提交前查看，以免提交测试或错误代码
有时开发人员共同修改同一个文件，可能导致冲突，这时，我们需要执行 git pull更新代码后修改冲突文件，然后执行 git add ,git commit,git push

有时我们需要会退到以前的版本：

git log #查看日志
git reset --hard <string> #回退
git reflog     #查看回到过去与最新版本之间的更新历史

git reset --hard <string> #回退到指定版本
分支开发：

git branch name  #创建分支
git branch  #查看当前所有的分支
git checkout master     #切换回master分支
git branch –d dev     #删除dev分支
git checkout –b dev  #创建dev分支 并切换到dev分支上
git merge dev   #在当前的分支上合并dev分支

一些其他的常用命令：

git remote 查看远程库的信息
git remote add origin https://www.github.com/...     #关联一个远程库
git push origin master  #把master分支推送到远程库对应的远程分支上
