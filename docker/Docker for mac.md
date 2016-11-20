
Docker for mac
============

参考文档[docker](https://docs.docker.com/docker-for-mac/)

## 版本检查

```
$ docker --version
Docker version 1.12.0, build 8eab29e

$ docker-compose --version
docker-compose version 1.8.0, build f3628c7

$ docker-machine --version
docker-machine version 0.8.0, build b85aac1
	
```

## 运行nginx
如果本地没有镜像会先下载 nginx 镜像
```
docker run -d -p 80:80 --name webserver nginx 
```

## 使用 `docker ps`命令查看正在运行的容器

```
$ docker stop webserver
$ docker start webserver
列出正在运行的容器信息
$ docker ps 
```

## 删除所有容器

```
docker rm `docker ps -a -q`
```

## 查询信息

```
docker info
```