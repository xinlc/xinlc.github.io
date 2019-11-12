---
title: Docker 安装 Jenkins
date: 2019-11-02 20:50:00
categories: Linux
tags:
  - linux
  - docker
  - jenkins
  - CI/CD
---

它来了，它来了，没错就是它， `Jenkins` 构建伟大，无所不能。 `Jenkins` 是开源 `CI&CD` 软件领导者，提供超过 1000 个插件来支持构建、部署、自动化，满足任何项目的需要。

<!--more-->

## 安装

未安装 `Docker` 可参考 [CentOS7 安装 Docker](https://xinlc.github.io/2019/09/15/back-end/linux/linux-install-docker/#more)

### 使用 `docker-compose` 安装 `Jenkins`：

```yaml
version: "3"

services:
  jenkins:
    image: jenkinsci/blueocean:latest
    privileged: true
    user: root
    ports:
      - "8080:8080"
      - "50000:50000"
    volumes:
      - /usr/share/zoneinfo/Asia/Shanghai:/etc/localtime:ro
      - ~/docker-data/jenkins_home:/var/jenkins_home
      - /var/run/docker.sock:/var/run/docker.sock
```

- `privileged: true` 提升容器权限。
- `user: root` 使用 root 用户。
- `~/docker-data/jenkins_home:/var/jenkins_home` `/var/jenkins_home` 目录为 Jenkins 工作目录，方便后续更新镜像后继续使用原来的工作目录。
- `/usr/share/zoneinfo/Asia/Shanghai:/etc/localtime:ro` 让容器使用和服务器同样的时间设置。
- `/var/run/docker.sock:/var/run/docker.sock` 容器内可以使用主机 Docker 守护进程通信。

### 启动

```bash
docker-compose up -d
```

### 查看 logs，会自动打印出密码

```bash
docker-compose logs -f
```

![1][1]

### 访问 `http://localhost:8080`

![2][2]

### 输入后台打印出的密码，继续，耐心等吧

如果一直在 Please wait while Jenkins is getting ready to work ...，需要配置代理

```bash
# 进入jenkins的工作目录，打开
vim ~/docker-data/jenkins/hudson.model.UpdateCenter.xml

# 把 `https://updates.jenkins.io/update-center.json` 改成 `http://mirror.xmission.com/jenkins/updates/update-center.json`

# 保存后，重启容器
docker-compose restart

```

其他镜像源

- 清华大学 https://mirrors.tuna.tsinghua.edu.cn/jenkins/
- 华为 https://mirrors.huaweicloud.com/jenkins/
- 腾讯云 https://mirrors.cloud.tencent.com/jenkins/
- 北京理工大 http://mirror.bit.edu.cn/jenkins/
- USTC http://mirrors.ustc.edu.cn/jenkins/

### 选择推荐安装

![3][3]

### 创建管理员账户

![4][4]

![5][5]

## 权限管理

1. 在 系统管理->管理用户->新建用户
2. 系统管理->全局安全配置, 注意添加一个 admin 用户

![6][6]

## 环境变量配置

如果找不到 docker 命令可以配置节点环境变量如下：

系统管理->节点管理->点击对应节点后的设置->环境变量

- `PATCH+LOCAL_BIN=/usr/bin`

## 在容器中安装软件

比如安装 NodeJS

```bash
# 进入容器
docker-compose exec jenkins bash

# 搜索软件, apk 是 Alpine 系统包管理工具
apk search node

# 安装 node & npm
apk add nodejs=10.14.2-r0
apk add npm=10.14.2-r0

```

> 不建议这样做，最好使用 Dockerfile 重新构建 Jenkins 镜像，或在 agent 使用 docker，参考：https://jenkins.io/doc/book/pipeline/docker/#dockerfile

## 安装常用插件

系统管理->插件管理

- Maven Integration plugin
- SSH Pipeline Steps
- Publish Over SSH

## 参考

- [jenkins](https://jenkins.io/zh/doc/)
- [jenkins installing](https://jenkins.io/zh/doc/book/installing/)
- [jenkins pipeline](https://jenkins.io/doc/pipeline/steps/workflow-basic-steps/)

[1]: /images/linux/docker-jenkins/1.jpg
[2]: /images/linux/docker-jenkins/2.jpg
[3]: /images/linux/docker-jenkins/3.jpg
[4]: /images/linux/docker-jenkins/4.jpg
[5]: /images/linux/docker-jenkins/5.jpg
[6]: /images/linux/docker-jenkins/6.jpg