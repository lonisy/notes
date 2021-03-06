
搭建Git服务器
============

- 首先要安装git

```
$ sudo yum install git
```
- 创建一个git用户

```
$ sudo adduser git

```
- 创建登录证书

收集所有需要登录的用户的公钥，就是他们自己的id_rsa.pub文件，把所有公钥导入到/home/git/.ssh/authorized_keys文件里，一行一个。

- 初始化Git仓库

先选定一个目录作为Git仓库，假定是/srv/sample.git，在/srv目录下输入命令：
```
$ sudo git init --bare sample.git
$ sudo git init --bare apiservice.git
$ sudo git init --bare uztapp.git
$ sudo git init --bare wck.html.git
```
Git就会创建一个裸仓库，***裸仓库*** 没有工作区，因为服务器上的Git仓库纯粹是为了共享，所以不让用户直接登录到服务器上去改工作区，并且服务器上的Git仓库通常都以.git结尾。然后，把owner改为git：

```
$ sudo chown -R git:git uztapp.git

```

- 禁用shell登录
  出于安全考虑，第二步创建的git用户不允许登录shell，这可以通过编辑/etc/passwd文件完成。找到类似下面的一行：

```
git:x:1001:1001:,,,:/home/git:/bin/bash
改为
git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell

```

- 克隆远程仓库
  现在，可以通过git clone命令克隆远程仓库了，在各自的电脑上运行：

```
$ git clone git@192.168.5.10:uztapp.git
$ git clone git@server:/srv/sample.git
Cloning into 'sample'...
warning: You appear to have cloned an empty repository.

git clone /home/git/quotes.git/ /data/quotes
```
- 将本地的仓库和远程的仓库进行关联
  git clone git@112.124.108.15:wck.html.git
```
$ git init
$ git remote add origin git@192.168.5.10:uztapp.git
$ git remote add origin git@www.lilei.org.cn:wck.html.git

git@114.55.225.47:apiservice.git

git remote add origin git@192.168.5.10:apiservice.git

git remote set-url --add all git@192.168.5.10:apiservice.git
```


* 初始建立一个bare repo

$ git init --bare

* 如果已有一个repo了，使用下面的方法将其转化为bare的

$ git config --bool core.bare true 

之后可删除除了repo根目录.git文件夹之外的所有文件，即只保留专用目录