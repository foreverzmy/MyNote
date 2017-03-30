# Docker

## 安装

* windows

windows 一般需要安装 docker toolbox，可到[官网](https://www.docker.com/products/docker-toolbox)下载。

## 安装镜像

* 搜索镜像

```
docker search centos
```

* 安装镜像

```
docker pull centos:latest
```

* 查看镜像运行情况

``` 
docker images centos
```

* 在容器下运行 shell bash

```
docker run -i -t centos /bin/bash
```

* 后台运行容器

```
docker run -d centos ping 8.8.8.8
```

* 进入后台容器的 shell bash

```
docker exec -ti images_name /bin/bash
```

* 检查容器

```
docker ps
```

* 停止容器

```
docker stop <CONTAINER ID>
```

* 查看容器日志

```
docker logs -f <CONTAINER ID>
```

* 删除所有容器

```
docker rm $(docker ps -a -q)
```

* 删除镜像

```
docker rmi <image id/name>
```

## docker 快捷键

* [ctrl + D]:这样会结束docker当前线程，容器结束。
* [ctrl + P]/[ctrl + Q]退出而不终止容器运行。