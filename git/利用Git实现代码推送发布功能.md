利用Git实现代码推送自动发布功能
============================

http://my.oschina.net/cxz001/blog/194196


+ 遇到一个问题, 钩子执行的时候权限的问题,这个时候需要在目标目录 给目录添加可执行权限

find . -mtime 95 | xargs -i mv {} test


find . -type f -size -900k | xargs -i mv {} test

find . -type f -size -900k -exec mv {} ./test/ \;
