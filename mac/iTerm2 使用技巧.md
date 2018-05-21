# iTerm 2 使用技巧

## iTerm2 实现 secureCRT 的克隆会话（session clone）功能
这样做的目的还解决了登陆跳板机的弊病，就是每次新开一个窗口连接跳板机就得重新输入PIN+TOKEN来登录跳板机。   
这样的实现类似于 Xshell 的 "复制 SSH 通道" 功能。

1、创建 cm_socket 文件     
`mkdir -p ~/.ssh/cm_socket`

2、编辑 config 文件    
`vi ~/.ssh/cm_socket/config`   
3、输入一下内容   
```
Host *
ControlMaster auto
ControlPath ~/.ssh/cm_socket/%r@%h:%p
```
4、重启终端


使用方法: 
首次打开跳板机，输入 PIN + TOKEN 后， 在新窗口再次登陆跳板机，无序输入 PIN + TOKEN
使用命令 command + t

注意点：如果没有奏效可能还需要对iTerms2做以下设置：Preference——Profiles——WorkingDirectory；选择reuse previous sessions’s directory

参考链接：(https://www.jianshu.com/p/086d4b3cc00a)[https://www.jianshu.com/p/086d4b3cc00a]

## iTerm2 实现快速登陆
即输入指定的服务器别名，实现快速登陆。

1、编辑config 文件  
`vi ~/.ssh/config`
2、输入一下内容  
``` 
Host myhost  
    HostName  192.168.9.20 
    User root  
    IdentityFile ~/.ssh/id_rsa  
    ServerAliveInterval 80  
```

使用方法: 
ssh myhost
