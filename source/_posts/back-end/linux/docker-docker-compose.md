---
title: Docker 三剑客之 Docker Compose
date: 2019-11-18 19:00:00
categories: Linux
tags:
  - docker
---

Docker Compose 是 Docker 官方编排（Orchestration）项目之一，负责快速的部署分布式应用。

<!--more-->

## 术语

服务 (service)：一个应用容器，实际上可以运行多个相同镜像的实例。

项目 (project)：由一组关联的应用容器组成的一个完整业务单元。

一个项目可以由多个服务（容器）关联而成，Compose 面向项目进行管理。

## 安装 docker-compose

运行此命令以下载 Docker Compose 的当前稳定版本：

```bash
# 下载
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# 对二进制文件应用可执行权限：
sudo chmod +x /usr/local/bin/docker-compose

```

## bash 补全命令

```bash
curl -L https://raw.githubusercontent.com/docker/compose/1.24.1/contrib/completion/bash/docker-compose > /etc/bash_completion.d/docker-compose
```

## 命令对象与格式

对于 Compose 来说，大部分命令的对象既可以是项目本身，也可以指定为项目中的服务或者容器。如果没有特别的说明，命令对象将是项目，这意味着项目中所有的服务都会受到命令影响。

执行 `docker-compose [COMMAND] --help` 或者 `docker-compose help [COMMAND]` 可以查看具体某个命令的使用格式。

docker-compose 命令的基本的使用格式是

```bash
docker-compose [-f=<arg>...] [options] [COMMAND] [ARGS...]
```

命令选项

- `-f, --file FILE` 指定使用的 Compose 模板文件，默认为 docker-compose.yml，可以多次指定。

- `-p, --project-name NAME` 指定项目名称，默认将使用所在目录名称作为项目名。

- `--x-networking` 使用 Docker 的可拔插网络后端特性

- `--x-network-driver DRIVER` 指定网络后端的驱动，默认为 bridge

- `--verbose` 输出更多调试信息。

- `-v, --version` 打印版本并退出。

## 常用命令

```bash
docker-compose up -d                               # 在后台运行
docker-compose -f xxx.yml up -d                    # 指定使用的 Compose 模板文件
docker-compose down                                # 会停止 up 命令所启动的容器，并移除网络, --volumes 移除数据卷
docker-compose pull                                # 拉取服务依赖的镜像
docker-compose start [SERVICE ...]                 # 启动项目中服务
docker-compose stop [SERVICE ...]                  # 停止项目中服务
docker-compose restart [SERVICE ...]               # 重启项目中服务
docker-compose logs --tail 100 -f [SERVICE ...]    # 查看最后100行log并跟随
docker-compose exec serviceA                       # 进入A服务容器
docker-compose scale web=3                         # 执行运行服务的数量，将启动3个容器运行web服务
```

## Compose 模板文件

[更多参考 docker-compose-file](https://docs.docker.com/compose/compose-file/)

```yaml
version: "3" # 使用docker-compose 第三版本语法

services:
  mysql: # 指定 service 名
    image: mysql:5.7 # 指定使用的镜像，默认从 docker hub
    container_name: mysql # 指定启动后的容器名
    ports: # 指定开放的端口号，主机:容器
      - "3306:3306"
    restart: always # docker 启动后，容器自启动
    environment: # 指定环境变量
      - MYSQL_ROOT_PASSWORD=root
    networks: # 指定网络
      - my-net
    volumes: # 定义数据卷所挂载路径设置 HOST:CONTAINER，ro 代表只读
      - /usr/share/zoneinfo/Asia/Shanghai:/etc/localtime:ro
      - ~/docker-data/mysql-data:/var/lib/mysql
      - ~/docker-data/mysql.conf.d:/etc/mysql/mysql.conf.d
    deploy: # 限制容器使用资源
      resources:
        limits:
          cpus: "0.5"
          memory: 2048M
    logging: # 指定 log 使用的驱动
      driver: "json-file"
      options:
        max-size: "20m"
        max-file: "2"

  web:
    image: nginx:latest
    restart: always
    depends_on:
      - mysql
    ports:
      - "80:80"
    networks:
      - my-net
    volumes:
      - /usr/share/zoneinfo/Asia/Shanghai:/etc/localtime:ro
      - /etc/timezone:/etc/timezone:ro
      - ~/docker-data/web/nginx/nginx.conf:/etc/nginx/nginx.conf
      - ~/docker-data/web/nginx/conf.d:/etc/nginx/conf.d
      - ~/docker-data/web/www:/usr/share/nginx/html
      - ~/docker-data/web/logs:/var/log/nginx

networks:
    my-net:
```

## 参考

- [docker-compose](https://docs.docker.com/compose/install/)
- [docker-compose CLI](https://docs.docker.com/compose/reference/overview/)
- [docker-compose-file](https://docs.docker.com/compose/compose-file/)