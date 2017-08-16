Git 介绍
---------------
Git 是一款免费且开源的分布式版本关系系统, 可以敏捷高效的处理任何或大或小的项目.


### Git 相关资料

1. 官方网站 https://git-scm.com/
2. Github https://github.com/
3. Gitlab https://about.gitlab.com/
4. 码云 http://git.oschina.net/
5. [Git 教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)


### Git 相关软件

1. [gitfor windows](https://git-for-windows.github.io/)
2. Windows/Mac OS X [SourceTree](https://www.sourcetreeapp.com/)

### Git 常用命令

```shell
$ git config --global user.name "lee"
$ git config --global user.email lee@163.com
$ git clone user@host:/path/project     # 克隆项目
$ git status         # 查看状态
$ git add <file>     # 建立跟踪
$ git commit         # 完成提交
$ git pull           # 更新代码
$ git push           # 推送至远程服务器
$ git diff           # 查看修改了哪些内容，推荐每次提交前查看，以免提交测试或错误代码
$ git log            # 查看日志
$ git reset --hard <string> # 回退到指定版本
$ git reflog                # 查看回到过去与最新版本之间的更新历史
$ git branch name           # 创建分支
$ git branch                # 查看当前所有的分支
$ git checkout master       # 切换回master分支
$ git branch –d dev         # 删除dev分支
$ git checkout –b dev       # 创建dev分支 并切换到dev分支上
$ git merge dev             # 在当前的分支上合并dev分支
$ git remote                # 查看远程库的信息
$ git remote add origin https://www.github.com/...     # 关联一个远程库    
$ git push origin master    # 把master分支推送到远程库对应的远程分支上    

```

### 配置文件

```shell
$ cat ~/.gitconfig   # 用户目录下面的配置文件
$ .git/config        # 项目 git 配置文件
$ .git/hooks         # 钩子文件夹
$ .gitignore         # 项目中忽略配置文件
```

### 专用名词 
Workspace：工作区        
Index / Stage：暂存区      
Repository：仓库区（或本地仓库）    
Remote：远程仓库    