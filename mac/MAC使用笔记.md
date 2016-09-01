
MAC OS X 使用笔记
=========================
以下内容为MAC操作系统的实用笔记,不定期更新

##删除 .DS_store 文件
```
Macintoshlocal:~ user$ find . -name ".DS_Store" -exec rm -rf {} \;
# find . -name '.DS_Store' -delete
```

##复制公钥到远程服务器

```
Macintoshlocal:~ user$ scp ~/.ssh/id_rsa.pub root@47.90.22.19:~/id_rsa.pub

[root@iZ62yhqg424Z ~]# cat id_rsa.pub > .ssh/authorized_keys
[root@iZ62yhqg424Z ~]# chmod 700 ~/.ssh
[root@iZ62yhqg424Z ~]# chmod 600 ~/.ssh/authorized_keys

```


##ssh代理设置

```
Macintoshlocal:~ user$ ssh -D 7070 root@47.90.22.19

Macintoshlocal:~ user$ ssh -qTfnN -D 7070 root@47.90.22.19 # 安全模式
Macintoshlocal:~ user$ killall ssh # 关闭客户端转发
```
如果代理停掉之后,再次使用,需要kill掉端口为7070的进程, 并重新开启代理

## MACOSX下查看某个端口被哪个程序占用及杀进程方法

```
Macintoshlocal:~ user$ sudo lsof -i :9000
COMMAND PID USER FD TYPE DEVICE SIZE/OFF NODE NAME
java 61342 a 313u IPv6 0x1111111111111 0t0 TCP *:cslistener (LISTEN)
然后根据PID杀进程：
Macintoshlocal:~ user$ sudo kill -9 61342
```


