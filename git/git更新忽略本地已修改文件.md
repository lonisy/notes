git更新忽略本地已修改文件
================

需要放弃本地的修改，用远程的库的内容
正确的做法应该是
```
git fetch --all
git reset --hard origin/master

```
git fetch 只是下载远程的库的内容，不做任何的合并git reset 把HEAD指向刚刚下载的最新的版本
