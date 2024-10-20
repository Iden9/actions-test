---
title: "关于Docker"
date: 2024-10-20
categories: ["docker"]
---

以下是 Docker 的一些基础操作总结，涵盖安装、镜像、容器、网络、数据管理等常见任务。



## Docker 基础操作

### 1. **安装 Docker**
   - [Docker 官方安装指南](https://docs.docker.com/get-docker/) 提供了各操作系统（Windows、macOS、Linux）的详细步骤。
   - **Linux（Ubuntu）安装示例**：
     ```bash
     sudo apt-get update
     sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
     curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
     sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
     sudo apt-get update
     sudo apt-get install docker-ce
     sudo systemctl status docker  # 检查 Docker 是否安装成功
     ```

### 2. **镜像操作**

   - **搜索镜像**：
     ```bash
     docker search <镜像名>
     ```
     示例：`docker search ubuntu`
   
   - **下载镜像**：
     ```bash
     docker pull <镜像名>:<标签>
     ```
     示例：`docker pull ubuntu:latest`
   
   - **查看本地镜像**：
     ```bash
     docker images
     ```

   - **删除镜像**：
     ```bash
     docker rmi <镜像ID>
     ```

### 3. **容器操作**

   - **运行容器**：
     ```bash
     docker run -d -p <宿主端口>:<容器端口> <镜像名>
     ```
     示例：`docker run -d -p 8080:80 nginx` 在后台运行一个 Nginx 容器，监听宿主机的 8080 端口。
   
   - **查看运行中的容器**：
     ```bash
     docker ps
     ```

   - **查看所有容器（包括已停止的）**：
     ```bash
     docker ps -a
     ```

   - **停止容器**：
     ```bash
     docker stop <容器ID>
     ```

   - **启动容器**：
     ```bash
     docker start <容器ID>
     ```

   - **删除容器**：
     ```bash
     docker rm <容器ID>
     ```

   - **进入正在运行的容器**：
     ```bash
     docker exec -it <容器ID> /bin/bash
     ```
     示例：`docker exec -it my_container /bin/bash` 进入容器的交互式 shell。

   - **查看容器日志**：
     ```bash
     docker logs <容器ID>
     ```

   - **查看容器详细信息**：
     ```bash
     docker inspect <容器ID>
     ```

### 4. **容器网络**

   - **查看网络**：
     ```bash
     docker network ls
     ```

   - **创建自定义网络**：
     ```bash
     docker network create <网络名>
     ```
     示例：`docker network create mynetwork`
   
   - **运行容器并连接到网络**：
     ```bash
     docker run -d --network <网络名> <镜像名>
     ```
     示例：`docker run -d --network mynetwork nginx`

### 5. **数据管理（挂载卷）**

   - **挂载数据卷**：
     ```bash
     docker run -v <宿主目录>:<容器目录> <镜像名>
     ```
     示例：`docker run -d -v /mydata:/data nginx` 将宿主机的 `/mydata` 目录挂载到容器的 `/data` 目录。

   - **查看所有卷**：
     ```bash
     docker volume ls
     ```

   - **删除卷**：
     ```bash
     docker volume rm <卷名>
     ```

### 6. **Dockerfile 构建镜像**

   - **编写 `Dockerfile`**：
     创建一个名为 `Dockerfile` 的文件，并添加以下内容：
     ```dockerfile
     # 使用基础镜像
     FROM ubuntu:latest

     # 安装一些软件
     RUN apt-get update && apt-get install -y vim

     # 复制文件到容器
     COPY ./myfile.txt /usr/src/myfile.txt

     # 运行时命令
     CMD ["echo", "Hello World!"]
     ```
   
   - **构建镜像**：
     ```bash
     docker build -t my-custom-image .
     ```

   - **查看构建的镜像**：
     ```bash
     docker images
     ```

### 7. **Docker 容器导入/导出**

   - **保存容器为镜像**：
     ```bash
     docker commit <容器ID> <镜像名>
     ```

   - **导出容器**：
     ```bash
     docker export <容器ID> > container.tar
     ```

   - **导入容器**：
     ```bash
     docker import < container.tar
     ```

### 8. **常见问题与调试**

   - **查看容器 CPU 和内存使用情况**：
     ```bash
     docker stats
     ```

   - **强制停止所有容器**：
     ```bash
     docker stop $(docker ps -q)
     ```

   - **删除所有已停止的容器**：
     ```bash
     docker rm $(docker ps -a -q)
     ```


通过这些基础操作，你可以方便地进行 Docker 容器的创建、运行、管理和调试。根据实际情况，可以进一步探索 Docker Compose、Kubernetes 等工具，来实现更复杂的应用部署和管理。