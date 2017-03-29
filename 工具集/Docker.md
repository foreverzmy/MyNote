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