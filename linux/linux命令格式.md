linux 命令格式
======================

#### 命令基本格式

命令 [选项] [参数]   
注意: 个别命令使用方式不遵循该格式   

#### 命令行解析

[root@localhost ~]#
root 用户    
localhost 主机名     
~ 用户的家目录   
\# 超级管理员   
$ 普通用户  

#### stat 命令详细查看文件的详细信息

```
[root@localhost ~]# stat package.xml
  File: "package.xml"
  Size: 3626      	Blocks: 8          IO Block: 4096   普通文件
Device: fd00h/64768d	Inode: 397680      Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1000/ UNKNOWN)   Gid: ( 1000/ UNKNOWN)
Access: 2016-08-04 15:03:49.199581988 +0800
Modify: 2012-06-13 09:44:07.000000000 +0800
Change: 2016-08-04 15:03:49.202551376 +0800
```

#### 文件目录权限

-r--r--r--   
-rw-r--r--  所属用户 所属组 其他人  
-rw-r--r-- root(所属用户) root(所属组) 大小 时间 名称

\-rw-r--r-- 文件   
drw-r--r--  目录  
其他类型 .....  



#### linux 常见目录

/根目录
/etc 配置文件保存目录   
/bin 命令保存目录 普通用户可以读取的命令   
/boot 启动目录 保存相关文件   
/home 普通用户的家目录   
/lib 系统库保存目录    
/mnt 系统挂载目录   
/media 挂载目录
/dev 设备文件目录  



#### 硬链接

- 拥有相同的i节点, 可以立即为同一个文件   
- 只能通过i节点来访问   
- 不能跨分区   
- 不能针对目录使用   

```
[root@localhost ~]# ln anaconda-ks.cfg  /tmp/ana.hard
[root@localhost ~]# ll
总用量 7688
-rw-------.  2(引用了两次) root root    1941 12月  1 2015 anaconda-ks.cfg
[root@localhost ~]# ll /tmp/ana.hard
-rw-------. 2(引用了两次) root root 1941 12月  1 2015 /tmp/ana.hard
两个文件都可以编辑,删除,实际针对的是同一个i节点存储
尽量避免使用硬链接
```

#### 软链接

+ 软连接文件的权限为 lrwxrwxrwx
+ 软连接文件有独立的i节点号,也会有自己的属性
+ 修改任意一个文件都改变  
+ 删除源文件,软连接不可以使用

```
[root@localhost ~]# ln -s anaconda-ks.cfg  t.link
[root@localhost ~]# ll
总用量 7688
-rw-------.  1 root root    1941 12月  1 2015 anaconda-ks.cfg
lrwxrwxrwx.  1 root root      15 8月  11 09:37 t.link -> anaconda-ks.cfg
```
