---
title: Docker
date: 2020-12-30 10:55:24
background: bg-[#488fdf]
tags:
  - container
  - virtual
categories:
  - 编程
intro: |
  这是一个 [Docker](https://docs.docker.com/get-started/) 快速参考备忘单。你可以在这里找到最常用的 Docker 命令。
plugins:
  - copyCode
---

## 入门指南 {.cols-2}

### 入门

在后台创建并运行一个容器

```shell script
$ docker run -d -p 80:80 docker/getting-started
```

---

- `-d` - 以分离模式运行容器
- `-p 80:80` - 将主机端口 80 映射到容器端口 80
- `docker/getting-started` - 要使用的镜像

{.marker-none}

在前台创建并运行一个容器

```shell script
$ docker run -it -p 8001:8080 --name my-nginx nginx
```

---

- `-it` - 交互式 bash 模式
- `-p 8001:8080` - 将主机端口 8001 映射到容器端口 8080
- `--name my-nginx` - 指定一个名称
- `nginx` - 要使用的镜像

{.marker-none}

### 常用命令

| 示例                                | 描述                                     |
| ----------------------------------- | ------------------------------------------------ |
| `docker ps`                         | 列出正在运行的容器                          |
| `docker ps -a`                      | 列出所有容器                              |
| `docker ps -s`                      | 列出正在运行的容器<br>_(包括 CPU / 内存)_ |
| `docker images`                     | 列出所有镜像                                  |
| `docker exec -it <container>  bash` | 连接到容器                          |
| `docker logs <container>`           | 显示容器的控制台日志                    |
| `docker stop <container>`           | 停止一个容器                                 |
| `docker restart <container>`        | 重启一个容器                              |
| `docker rm <container>`             | 删除一个容器                               |
| `docker port <container>`           | 显示容器的端口映射                   |
| `docker top <container>`            | 列出进程                                   |
| `docker kill <container>`           | 杀死一个容器                                 |

参数 `<container>` 可以是容器 ID 或名称

## Docker 容器 {.cols-2}

### 启动与停止

| 描述               | 示例                             |
| ------------------------- | ----------------------------------- |
| `docker start my-nginx`   | 启动                            |
| `docker stop my-nginx`    | 停止                            |
| `docker restart my-nginx` | 重启                            |
| `docker pause my-nginx`   | 暂停                            |
| `docker unpause my-nginx` | 取消暂停                          |
| `docker wait my-nginx`    | 阻塞容器                |
| `docker kill my-nginx`    | 发送 SIGKILL 信号                   |
| `docker attach my-nginx`  | 连接到现有容器 |

### 信息

| 示例                   | 描述                            |
| ------------------------- | -------------------------------------- |
| `docker ps`               | 列出正在运行的容器                |
| `docker ps -a`            | 列出所有容器                    |
| `docker logs my-nginx`    | 容器日志                         |
| `docker inspect my-nginx` | 检查容器                  |
| `docker events my-nginx`  | 容器事件                      |
| `docker port my-nginx`    | 公共端口                           |
| `docker top my-nginx`     | 运行中的进程                      |
| `docker stats my-nginx`   | 容器资源使用情况                  |
| `docker diff my-nginx`    | 列出对容器所做的更改。 |

### 创建

```yaml
docker create [选项] 镜像
  -a, --attach               # 附加 stdout/err
  -i, --interactive          # 附
  -t, --tty                  # pseudo-tty
      --name NAME            # name your image
  -p, --publish 5000:5000    # port map (host:container)
      --expose 5432          # expose a port to containers
  -P, --publish-all          # publish all ports
      --link container:alias # linking
  -v, --volume `pwd`:/app    # mount (absolute paths needed)
  -e, --env NAME=hello       # env vars
```

#### Example

```shell script
$ docker create --name my_redis --expose 6379 redis:3.0.2
```

### Manipulating

Renaming a Container

```shell script
docker rename my-nginx my-nginx
```

Removing a Container

```shell script
docker rm my-nginx
```

Updating a Container

```shell script
docker update --cpu-shares 512 -m 300M my-nginx
```

## Docker Images {.cols-2}

### Manipulating

| `Example`                          | Description                     |
| ---------------------------------- | ------------------------------- |
| `docker images`                    | Listing images                  |
| `docker rmi nginx`                 | Removing an image               |
| `docker load < ubuntu.tar.gz`      | Loading a tarred repository     |
| `docker load --input ubuntu.tar`   | Loading a tarred repository     |
| `docker save busybox > ubuntu.tar` | Save an image to a tar archive  |
| `docker history`                   | Showing the history of an image |
| `docker commit nginx`              | Save a container as an image.   |
| `docker tag nginx eon01/nginx`     | Tagging an image                |
| `docker push eon01/nginx`          | Pushing an image                |

### Building Images

```shell script
$ docker build .
$ docker build github.com/creack/docker-firefox
$ docker build - < Dockerfile
$ docker build - < context.tar.gz
$ docker build -t eon/my-nginx .
$ docker build -f myOtherDockerfile .
$ curl example.com/remote/Dockerfile | docker build -f - .
```

## Docker Networking {.cols-2}

### Manipulating

Removing a network

```shell script
docker network rm MyOverlayNetwork
```

Listing networks

```shell script
docker network ls
```

Getting information about a network

```shell script
docker network inspect MyOverlayNetwork
```

Connecting a running container to a network

```shell script
docker network connect MyOverlayNetwork nginx
```

Connecting a container to a network when it starts

```shell script
docker run -it -d --network=MyOverlayNetwork nginx
```

Disconnecting a container from a network

```shell script
docker network disconnect MyOverlayNetwork nginx
```

### Creating Networks

```shell script
docker network create -d overlay MyOverlayNetwork

docker network create -d bridge MyBridgeNetwork

docker network create -d overlay \
  --subnet=192.168.0.0/16 \
  --subnet=192.170.0.0/16 \
  --gateway=192.168.0.100 \
  --gateway=192.170.0.100 \
  --ip-range=192.168.1.0/24 \
  --aux-address="my-router=192.168.1.5" \
  --aux-address="my-switch=192.168.1.6" \
  --aux-address="my-printer=192.170.1.5" \
  --aux-address="my-nas=192.170.1.6" \
  MyOverlayNetwork
```

## Clean Up {.cols-2}

### Clean All

Cleans up dangling images, containers, volumes, and networks (ie, not associated with a container)

```shell
docker system prune
```

---

Additionally, remove any stopped containers and all unused images (not just dangling images)

```shell
docker system prune -a
```

### Containers

Stop all running containers

```shell
docker stop $(docker ps -a -q)
```

Delete stopped containers

```shell
docker container prune
```

### Images

Remove all dangling (not tagged and is not associated with a container) images:

```shell
docker image prune
```

Remove all images which are not used by existing containers

```shell
docker image prune -a
```

### Volumes

```shell
docker volume prune
```

Remove all volumes not used by at least one container

## Miscellaneous {.cols-2}

### Docker Hub

| Docker Syntax               | Description                         |
| --------------------------- | ----------------------------------- |
| `docker search search_word` | Search docker hub for images.       |
| `docker pull user/image   ` | Downloads an image from docker hub. |
| `docker login             ` | Authenticate to docker hub          |
| `docker push user/image   ` | Uploads an image to docker hub.     |

### Registry commands {.row-span-3}

Login to a Registry

```shell script
$ docker login
$ docker login localhost:8080
```

Logout from a Registry

```shell script
$ docker logout
$ docker logout localhost:8080
```

Searching an Image

```shell script
$ docker search nginx
$ docker search nginx --stars=3 --no-trunc busybox
```

Pulling an Image

```shell script
$ docker pull nginx
$ docker pull eon01/nginx localhost:5000/myadmin/nginx
```

Pushing an Image

```shell script
$ docker push eon01/nginx
$ docker push eon01/nginx localhost:5000/myadmin/nginx
```

### Batch clean

| Example                             | Description             |
| ----------------------------------- | ----------------------- |
| `docker stop -f $(docker ps -a -q)` | Stopping all containers |
| `docker rm -f $(docker ps -a -q)`   | Removing all containers |
| `docker rmi -f $(docker images -q)` | Removing all images     |

### Volumes

Check volumes

```shell script
$ docker volume ls
```

Cleanup unused volumes

```shell script
$ docker volume prune
```
