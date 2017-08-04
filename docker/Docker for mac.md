
Docker for mac
============

参考文档[docker](https://docs.docker.com/docker-for-mac/)



## 版本检查

```
$ docker --version
Docker version 1.12.0, build 8eab29e

$ docker-compose --version
docker-compose version 1.8.0, build f3628c7

Compose是用于定义和运行复杂Docker应用的工具。
在安装 Compose之前,你需要先安装好 Docker 

$ docker-machine --version
docker-machine version 0.8.0, build b85aac1
	
```

## 运行nginx
如果本地没有镜像会先下载 nginx 镜像
```
docker run -d -p 80:80 --name webserver nginx 
```

## Docker 镜像管理

```
查找镜像 https://hub.docker.com/

镜像在 mac os 中的存放位置
/Users/${USER}/Library/Containers/com.docker.docker/Data

$ docker search '镜像关键词' // 搜索镜像
$ docker search sinatra // 查找镜像
$ docker search nginx // 查找

$ docker pull training/sinatra // 类似命名空间的镜像名, 获取查到的镜像
$ docker run -t -i training/sinatra /bin/bash // 使用获取的镜像运行容

$ docker commit -m '变动信息' -a '作者' 4742b9cedb77(容器 ID) centos:6.8.1  // 提交容器内的变动
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
centos              6.8.1               180e86d806cd        11 seconds ago      218.9 MB
centos              6.8                 0cd976dc0a98        3 months ago        194.5 MB

$ docker pull 镜像
$ docker images // 显示本地的 docker 镜像
$ docker rmi -f 05a60462f8ba // 根据镜像 ID 强制删除本地指定的景象

#docker help pull
#Usage:	docker pull [OPTIONS] NAME[:TAG|@DIGEST]

# docker pull centos:7 // 获取centos版本7 docker镜像

使用 docker commit 命令进行镜像的修改太繁琐
利用Dockerfile 使用 docker build 命令,从头开始构建新的图像。

$ docker build -t ouruser/sinatra:v2 .  编辑Dockerfile 后构建镜像
[ouruser/sinatra] 镜像命名规范,名称,标签

镜像不能超过127层,Dockerfile内的操作
$ docker run -t -i ouruser/sinatra:v2 /bin/bash 运行构建成功的镜像

给镜像设置标签
$ docker tag 5db5f8471261 ouruser/sinatra:devel
$ docker images --digests | head // 查看镜像摘要
$ docker history centos:centos7 用docker history看你的主机上的镜像层的大小
```

## Docker Container manage容器管理

```
$ docker run -i -t ubuntu /bin/bash // 创建一个交互容器,并指定使用的 shell
$ docker run -i -t centos:6.8 echo "hello word!" // 创建容器并输出 hello word


$ docker run -d -p 2222:22 --name base lee/centos:7 // 必须有服务运行才可以用
$ docker run -d -p 2222:22 --name test lee/centos-nginx   2222 宿主机的端口 : 22容器端口
$ docker run -it -p 8080:80 --name test lee/centos-nginx  8080 宿主机的端口 : 80容器端口
$ docker run -it centos /bin/bash // 交互测试 
$ docker rm `docker ps -a |awk '{print $1}' | grep [0-9a-z]` // 批量删除容器

当使用 -P 标记时，Docker 会随机映射一个 49000~49900 的端口到内部容器开放的网络端口。
$ sudo docker run -d -P training/webapp python app.py
$ sudo docker ps -l
CONTAINER ID  IMAGE                   COMMAND       CREATED        STATUS        PORTS                    NAMES
bc533791f3f5  training/webapp:latest  python app.py 5 seconds ago  Up 2 seconds  0.0.0.0:49155->5000/tcp  nostalgic_morse

使用交互模式基于lee/nginx镜像启动一个容器, 并通过 -v 参数把本地目录 ~/Projects 映射到容器中 /data 目录
$ docker run -v ~/Projects:/data -v `pwd`/www:/www -it lee/nginx
启动后直接进入 bash

docker run 运行的容器。
ubuntu 就是你想运行的映像。
-t 标志分配新的容器内伪终端或终端。
-i标志允许您通过抓住标准输入（使交互式连接STDIN容器）。
/bin/bash 我们推出容器内的Bash shell中。

运行一个对外提供服务的容器
$ docker run -d -P training/webapp python app.py 自动映射端口
$ docker run -d -p 80:5000 training/webapp python app.py 指定映射端口
该-d标志在后台运行容器（如所谓的守护进程）。 
该-P标志在容器内的任何所需的网络端口映射到你的主机。这允许您查看Web应用程序。
该training/webapp图像是包含一个简单的Python瓶Web应用程序预建的图像。
其余的论据是，它是容器内运行的命令。该python app.py命令将启动Web应用程序。


$ docker ps -a // 查看所有容器包括停止状态的容器
$ docker ps -a -q // 查看所有容器包括停止状态的容器,但只列出容器ID
$ docker ps -l // 查看最新创建的容器
$ docker ps -n=x // 查看最后创建的 X 个容器
$ docker rm `docker ps -a -q` // 删除所有容器
$ docker rm 'Container ID' // 删除指定容器ID 的容器
$ docker start 容器名或容器ID来启动容器 // 启动容器
$ docker stop 容器名或容器ID // 终止容器
$ docker rm 容器名 // 删除容器
$ docker kill 容器名或容器ID // 强制停止容器

// 例
$ docker stop webserver
$ docker start webserver

CONTAINER ID：容器ID，唯一标识容器 
IMAGE：创建容器时所用的镜像 
COMMAND：在容器最后运行的命令 
CREATED：容器创建的时间 
STATUS：容器的状态（你会看到UPXXX，表示运行状态） 
PORTS：对外开放的端口号 
NAMES：容器名（也具有唯一性，docker是不允许创建容器名相同的容器的） 


$ docker ps -l
-l 标志是显示最后一个容器的详细信息

$ docker port nostalgic_morse 5000
快捷指定暴露端口

$ docker logs -f nostalgic_morse
查看容器日志, tail -f 类似

$ docker top nostalgic_morse
查看容器的进程

$ docker inspect nostalgic_morse
查询容器信息

$ docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' nostalgic_morse
查询指定信息

进入正在运行中的容器
# docker exec -it 9a91c6f5c228(容器 ID) /bin/bash

$ docker run -d -P web/nginx  
开放所有端口,映射到宿主机的随机端口上

$ docker run -itd --net=host --name docker_host2 ubuntu-base:v3  
设定网络模式为 host 模式,并指定容器名 和 所使用的镜像

$ docker stats 容器名/容器id
在宿主机查看docker使用cpu、内存、网络、io情况

$ docker attach contener容器
```

## 查询信息

```
docker info
```


## Docker-compose 使用

#### 基本用法

Compose是Docker的服务编排工具，主要用来构建基于Docker的复杂应用，Compose 通过一个配置文件来管理多个Docker容器，非常适合组合使用多个容器进行开发的场景。

服务编排工具使得Docker应用管理更为方便快捷。 Compose网站：[https://docs.docker.com/compose/](https://docs.docker.com/compose/)

[参考资料](http://www.cnblogs.com/52fhy/p/5991344.html)

[参考资料](http://dockone.io/article/834)

```
$ docker-compose up  // 默认是前台运行并打印日志到控制台。
$ docker-compose up -d // 后台运行
$ docker-compose ps // 查看状态
$ docker-compose stop // 停止服务
$ docker-compose restart // 重启服务

```



## Dockerfile 参考手册

####  语法示例
Dockerfile语法由两部分构成，注释和命令+参数

```
# Line blocks used for commenting
command argument argument ..

# Print "Hello docker!"
RUN echo "Hello docker!"
```
####  Dockerfile 命令

Dockerfile有十几条命令可用于构建镜像，下文将简略介绍这些命令。

####  ADD 命令

ADD命令有两个参数，源和目标。它的基本作用是从源系统的文件系统上复制文件到目标容器的文件系统。如果源是一个URL，那该URL的内容将被下载并复制到容器中。

```
# Usage: ADD [source directory or URL] [destination directory]
# ADD /宿主系统文件或者目录 /容器目录或者文件

ADD /my_app_folder /my_app_folder 
```

#### CMD 命令

和RUN命令相似，CMD可以用于执行特定的命令。和RUN不同的是，这些命令不是在镜像构建的过程中执行的，而是在用镜像构建容器后被调用。

```
# Usage 1: CMD application "argument", "argument", ..
CMD "echo" "Hello docker!"

["/bin/bash", "-c", "echo hello"]

CMD echo hello
<=>
ENTRYPOINT ["echo","hello"]　

CMD:支持三种格式
1.CMD ["executable","param1","param2"] 使用 exec 执行，推荐方式；
2.CMD command param1 param2 在 /bin/sh 中执行，提供给需要交互的应用；
3.CMD ["param1","param2"] 提供给 ENTRYPOINT 的默认参数；
```

####  ENTRYPOINT 命令

ENTRYPOINT 帮助你配置一个容器使之可执行化，如果你结合CMD命令和ENTRYPOINT命令，你可以从CMD命令中移除“application”而仅仅保留参数，参数将传递给ENTRYPOINT命令。

```
# Usage: ENTRYPOINT application "argument", "argument", ..
# Remember: arguments are optional. They can be provided by CMD
# or during the creation of a container.
ENTRYPOINT echo
# Usage example with CMD:
# Arguments set with CMD can be overridden during *run*
CMD "Hello docker!"
ENTRYPOINT echo
```

####  ENV 命令

ENV命令用于设置环境变量。这些变量以”key=value”的形式存在，并可以在容器内被脚本或者程序调用。这个机制给在容器中运行应用带来了极大的便利。

```
# Usage: ENV key value
ENV SERVER_WORKS 4
ENV NGINX_VERSION 1.12.1
ENV PHP_VERSION 7.1
ENV PATH /usr/local/postgres-$PG_MAJOR/bin:$PATH
```

#### EXPOSE

EXPOSE用来指定端口，使容器内的应用可以通过端口和外界交互。

```
# Usage: EXPOSE [port]
EXPOSE 8080
```

#### FROM

FROM命令可能是最重要的Dockerfile命令。改命令定义了使用哪个基础镜像启动构建流程。基础镜像可以为任意镜像。如果基础镜像没有被发现，Docker将试图从Docker image index来查找该镜像。

**FROM命令必须是Dockerfile的首个命令**。

```
# Usage: FROM [image name]
FROM ubuntu 
```

####  MAINTAINER

我建议这个命令放在Dockerfile的起始部分，虽然理论上它可以放置于Dockerfile的任意位置。这个命令用于声明作者，并应该放在FROM的后面。

```
# Usage: MAINTAINER [name]
MAINTAINER authors_name 
```

#### RUN

RUN命令是Dockerfile执行命令的核心部分。它接受命令作为参数并用于创建镜像。不像CMD命令，RUN命令用于创建镜像（在之前commit的层之上形成新的层）。

```
# Usage: RUN [command]
RUN aptitude install -y riak
```

#### USER

USER命令用于设置运行容器的UID。

```
# Usage: USER [UID]
USER 751
```

#### VOLUME

VOLUME命令用于让你的容器访问宿主机上的目录。

**好像此属性在Dockerfile中指定并没有什么意义**

```
# Usage: VOLUME ["/dir_1", "/dir_2" ..]
VOLUME ["/my_files"]
```

#### WORKDIR

WORKDIR命令用于设置CMD指明的命令的运行目录。

```
# Usage: WORKDIR /path
WORKDIR ~/
```

#### 使用 Dockerfile

使用Dockerfiles和手工使用Docker Daemon运行命令一样简单。脚本运行后输出为新的镜像ID。

```
# Build an image using the Dockerfile at current location
# Example: sudo docker build -t [name] .
# Help: sudo docker build --help 
sudo docker build -t 镜像名(可以使用命名空间) . 
-t 参数 后面加要创建的镜像名 
-t 名字:标签


docker-compose up -d
docker-compose logs -f

```





## 参考文档

[http://www.open-open.com/lib/view/open1435671611966.html](http://www.open-open.com/lib/view/open1435671611966.html)

https://c.163.com/

+ [参考](http://os.51cto.com/art/201409/451117.htm)

http://www.simapple.com/319.html



## 网易蜂巢



docker pull hub.c.163.com/library/nginx:1.12.0-alpine