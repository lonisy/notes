
配置git使其可以同时push到多个远程仓库
=================



config 中配置了两个远程仓库。想在终端下一句 git push 同时把代码提交到两个仓库，该怎么做？

1. 新的Git, Git 多了一项设置，使得你可以为一个 remote 设置多个 pushurl。

```
git remote set-url --add --push origin git@192.168.5.10:soho.git
```

2. config 中配置`remote "origin"` 就变成类似如下的结构

```
[remote "origin"]
        url = git@github.com:SegmentFault/XXX.git
        fetch = +refs/heads/*:refs/remotes/origin/*
        pushurl = git@github.com:SegmentFault/XXX.git
        pushurl = git@gitlab.com:root/XXX.git
```