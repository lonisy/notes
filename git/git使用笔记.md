
git使用笔记
=========

```
[root@iZ11knikeskZ public_html]# git push
To /home/git/yhp2p.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to '/home/git/yhp2p.git'
To prevent you from losing history, non-fast-forward updates were rejected
Merge the remote changes before pushing again.  See the 'Note about
fast-forwards' section of 'git push --help' for details.
```

git仓库中已经有一部分代码，所以它不允许你直接把你的代码覆盖上去。于是你有2个选择方式：


1，强推，即利用强覆盖方式用你本地的代码替代git仓库内的内容

git push -f

2，先把git的东西fetch到你本地然后merge后再push

$ git fetch

$ git merge

这2句命令等价于
git pull





git push origin local_branch:remote_branch

这个操作，local_branch必须为你本地存在的分支，remote_branch为远程分支，如果remote_branch不存在则会自动创建分支。

类似，git push origin :remote_branch，local_branch留空的话则是删除远程remote_branch分支。