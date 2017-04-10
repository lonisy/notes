
Git库第一次提交代码
=============
第一次往自己或者别人在git上新建的git库里提交代码

## Git全局设置

> git config --global user.name "用户名"
> git config --global user.email "邮箱"

git的全局配置，存储于$HOME/.gitconfig 里，这里的配置影响当前用户的所有git repo。

## 创建git仓库

> git init
> git add .
> git commit -m "first commit"
> git remote add origin https://github.com/lonisy/test.git
> git push -u origin master

## 如果已有项目

> git remote add origin https://github.com/lonisy/test.git
> git push -u origin master

