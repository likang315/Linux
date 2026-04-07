### Docker

------

[TOC]

##### 01：概述

- 一种**轻量级的虚拟化技术**，它让**应用程序及其依赖环境可以被打包成一个标准化的单元**，在任何地方都能一致地运行。
  - 类似于：集装箱运输。
- 作用：无论你的应用是用 Python、Java 什么语言写的，需要什么样的依赖库和环境，一旦被打包成 **Docker 镜像**，就可以用同样的方式在**任何支持 Docker 的机器上运行**。

##### 02：Docker vs 虚拟机

| 特性     | 虚拟机（VM）                          | Docker 容器                           |
| :------- | :------------------------------------ | :------------------------------------ |
| 架构     | 每个 VM 包含完整操作系统（软件+硬件） | 共享宿主机 OS 内核                    |
| 启动速度 | 分钟级                                | 秒级                                  |
| 资源占用 | 高（内存、磁盘大）                    | 低（轻量级）                          |
| 隔离性   | 强（硬件级）                          | 进程级（通过 Linux namespace）        |
| 适用场景 | 运行不同操作系统                      | 快速部署微服务、CI/CD、开发环境标准化 |

##### 03：优势

1. 环境一致性；
2. 秒级启动；
3. 资源效率高，按需分配；
4. Docker 完美契合 DevOps 的工作流程；

##### 04：安装 Docker

###### Mac Homebrew 安装

```shell
$ brew install --cask docker
# 查看安装 docker 版本
$ docker version
$ docker info
# 运行一个 Nginx 服务器
$ docker run -d -p 80:80 --name webserver nginx
```

##### 05：基本概念

###### Docker镜像

- 是一个只读的模板，包含了运行应用所需的一切：代码、运行时、库、环境变量和配置文件。
- 镜像标识
  - 格式：`[仓库地址/]仓库名[:标签]`

###### 容器

- 容器是镜像的运行实例，应用实际运行的载体。
- 容器的本质
  - 容器的本质是一个特殊的进程，通过 Linux 内核的 **Namespace** 技术实现。
    - **进程空间**：容器看不到宿主机上的其他进程。
    - **网络**：容器拥有独立的 IP、端口等网络资源。
    - **文件系统**：容器拥有独立的 root 目录。
    - **用户**：容器内的 root 用户不等于宿主机的 root 用户。
- 容器的存储层
  - 当容器运行时，Docker 会在镜像的只读层之上创建一个 **可写层** (容器存储层)：Copy-on-Write：写时复制
    - 当容器需要修改镜像层中的文件时，Docker 将该文件 **复制** 到容器存储层，在容器层中进行修改，原始镜像层保持不变。
  - **容器存储层与容器生命周期绑定。**

###### 容器的生命周期

- <img src="/https://github.com/likang315/Linux/blob/master/Linux-%E8%BF%90%E7%BB%B4/photos/docker-lifetime.png" alt="docker-lifetime" style="zoom:30%;" />

  ```shell
  ## 创建并启动容器（最常用）
  $ docker run nginx
  
  ## 分步操作
  $ docker create nginx    # 创建容器（不启动）
  $ docker start abc123    # 启动容器
  
  ## 停止容器
  $ docker stop abc123     # 优雅停止（发送 SIGTERM，等待后发送 SIGKILL）
  $ docker kill abc123     # 强制停止（直接发送 SIGKILL）
  
  ## 暂停/恢复（不常用，但有时有用）
  $ docker pause abc123    # 暂停容器内所有进程
  $ docker unpause abc123  # 恢复
  
  ## 删除容器
  $ docker rm abc123       # 删除已停止的容器
  $ docker rm -f abc123    # 强制删除运行中的容器
  ```

###### 仓库

- Docker Registry 是存储和分发 Docker 镜像的服务。

- Registry、仓库、标签的关系

  - | 概念       | 说明               | 示例       |
    | ---------- | ------------------ | ---------- |
    | Registry   | 存储镜像的服务     | Docker Hub |
    | Repository | 同一软件镜像的集合 | 仓库       |
    | Tag        | 仓库内的版本标识   | Lastest    |

  - ```shell
    ## 完整格式
    registry.example.com/mycompany/myapp:v1.2.3
    │                    │         │     │
    │                    │         │     └── 标签
    │                    │         └── 仓库名
    │                    └── 用户名/组织名
    └── Registry 地址
    ```

- Docker Hub：最大的公共 Registry

- 镜像加速器

  - ```shell
    # 文件目录：/etc/docker/daemon.json
    {
      "registry-mirrors": [
        "https://hub.atomgit.com"
      ]
    }
    # 重启服务
    $ sudo systemctl daemon-reload
    $ sudo systemctl restart docker
    ```

##### 06：使用镜像

- 拉取镜像

  - ```shell
    $ docker pull [选项] [Registry地址/]仓库名[:标签]
    ```

- 列出镜像

  - ```shell
    $ docker image
    ```

- 过滤镜像

  - ```shell
    ## 列出所有 ubuntu 镜像
    $ docker images ubuntu
    ```

- 删除本地镜像

  - ```shell
    $ docker image rm [选项] <镜像1> [<镜像2> ...]
    ```

###### Dockerfile 定制镜像

-  是一个文本文件，其内包含了一条条的 **指令 (Instruction)**，每一条指令构建一层，因此每一条指令的内容，就是描述该层应当如何构建。

- 手动构键 Dockerfile

  - 建立一个文本文件，并命名为 `Dockerfile`：

    - ```shell
      $ mkdir mynginx
      $ cd mynginx
      $ touch Dockerfile
      
      # 文件内容为：
      
      FROM nginx  # 指定基础镜像
      # RUN 指令：执行命令行命令的
      RUN echo '<h1>Hello, Docker!</h1>' > /usr/share/nginx/html/index.html
      
      $ docker build [选项] <上下文路径/URL/->
      ```

- 实现原理（分层设计）
  - Docker 镜像并不是一个单纯的文件，而是由一组文件系统叠加构成的。
  - 最底层的镜像为 **基础镜像 (Base Image)**，通常是各种 Linux 发行版的 root 文件系统，如 Ubuntu、Debian等。当我们**在基础镜像之上构建新的镜像时** (例如安装了 Nginx)，Docker 并不是复制一份基础镜像，而是**在基础镜像之上，新建一个层 (Layer)**，并在该层中仅记录为了安装 Nginx 而发生的文件变更 (添加、修改、删除)。
  - **复用**：如果多个镜像都基于同一个基础镜像 (例如都基于 `ubuntu:24.04`)，那么宿主机只需要下载一份 `ubuntu:24.04`，所有镜像都可以共享它。
  - **轻量**：镜像仅仅记录了与基础镜像的差异，因此体积非常小。

##### 07：操作容器

启动

- ```shell
  docker run [选项] 镜像 [命令] [参数...]
  # 示例
  $ docker run -d ubuntu:24.04 /bin/echo 'Hello world'
  ```

终止

```shell
$ docker stop 容器名或ID 		#优雅停止
$ docker kill 容器名或ID    #强制停止
```

进入容器

```shell
## 进入容器并启动交互式 shell
$ docker exec -it 容器名 /bin/bash

## 退出，容器仍在运行！
```

删除

```shell
$ docker rm mycontainer
```

##### 08：Dockerfile 指令

- 相比编写 Bash 脚本的思维（"按顺序执行这些命令"），Dockerfile 的思维应该是（"这一层镜像应该如何构建，下一层如何分层"）。
  - **合并命令**：一个 `RUN apt-get update && apt-get install ...` 应该写在一起，而不是分开成多个 `RUN` 指令，因为它们是同一个"层"的逻辑。
  - **选择合适的指令**：`COPY` vs `ADD`这些选择不是随意的，而是根据镜像分层的语义来决定的。
  - **优化镜像大小**：最后才清理缓存、删除临时文件，让这些"瘦身"操作在同一层完成。
- Dockerfile 一般分为四部分：基础镜像信息、维护者信息、**镜像操作指令**和**容器启动时执行指令**。

###### RUN 执行指令

- 用于在镜像构建阶段执行命令来修改镜像。它在 当前镜像层 之上创建一个新层，执行指定的命令，并提交结果。

- ```
  RUN <command> 
  ```

###### COPY 复制文件

- 构建镜像时，将**构建上下文（Dockerfile 所在目录及其子目录）中的文件或目录复制到容器内的指令**。它是处理应用代码、配置文件最常用的方式。

- ```shell
  COPY [选项] <源路径>... <目标路径>
  $ COPY package.json /app/
  ```

###### CMD 容器启动命令

- 用于指定容器启动时默认执行的命令。它定义了容器的 “主进程”。

- ```
  CMD echo "Hello World"
  ```

###### ENTRYPOINT 入口点

- 指定容器启动时运行的入口程序。

- ```
  ENTRYPOINT 命令 参数
  ```

###### ENV 环境变量设置

- ```shell
  ## 格式一：单个变量
  ENV <key> <value>
  
  ## 格式二：多个变量（推荐）
  ENV <key1>=<value1> <key2>=<value2> ...
  ```

###### EXPOSE 暴露端口

- 声明容器运行时提供服务的端口。这是一个 **文档性质的声明**，告诉使用者容器会监听哪些端口。

- ```shell
  EXPOSE <端口> [<端口>/<协议>...]
  ```

















