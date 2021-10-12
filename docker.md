# Docker 笔记 

## 1. 安装Docker

1. 移除旧的文件

```shell
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine

```

2. 安装

   - 在新主机上首次安装 Docker Engine-Community 之前，需要设置 Docker 仓库。之后，您可以从仓库安装和更新 Docker。

   - 设置仓库

     安装所需的软件包。yum-utils 提供了 yum-config-manager ，并且 device mapper 存储驱动程序需要 device-mapper-persistent-data 和 lvm2。

     ```shell
     sudo yum install -y yum-utils \
       device-mapper-persistent-data \
       lvm2
     ```

   - 设置稳定的仓库

     ```shell
     sudo yum-config-manager \
         --add-repo \
         http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
     ```

   - 卸载

     ```shell
     # 删除安装包
     yum remove docker-ce
     rm -rf /var/lib/docker
     ```

     

## 2. 基本命令

1. 启动停止

   ```shell
   systemctl start docker
   systemctl stop docker
   ```

2. 交互的容器

   ````shell
   docker run -i -t centos:7 /bin/bash
   -t：在新容器内指定一个伪终端或终端
   -i：允许你对容器内的标准输入进行交互
   centos:7 要运行的镜像，首先查找本机上镜像，然后在Docker Hub下载公共镜像
   /bin/bash：启动镜像中的要用的一个程序，用shell进行执行。
   
   ````

3. 后台执行

   ```SHELL
   runoob@runoob:~$ docker run -d centos:7 /bin/bash -c "while truel;"
   2b1b7a428627c51ab8810d541d759f072b4fc75487eed05812646b8534a2fe63
   # 其中生成一个容器的ID，这个ID可以用来查看遇到了什么
   ```

4. 查看运行的镜像

   ```shell
   [root@zhuRoot ~]# docker ps
   CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
   
   CONTAINER ID:容器ID
   IMAGE：使用镜像
   COMMAND: 启动容器时运行的命令
   CREATED: 容器的创建时间
   STATUS: 容器状态
   状态有7种：
       created（已创建）
       restarting（重启中）
       running 或 Up（运行中）
       removing（迁移中）
       paused（暂停）
       exited（停止）
       dead（死亡）
   PORTS: 容器的端口信息和使用的连接类型（tcp\udp）
   NAMES: 自动分配的容器名称
   
   # 停止容器运行，可以使用名称NAMES或者CONTAINER ID
   [root@zhuRoot ~]# docker stop trusting_euclid
   trusting_euclid
   ```

5. 容器使用

   ```shell
   # 查看容器状态
   docker stats 
   # 启动容器
   docker run -it centos:7 /bin/bash
   # 查看已经停止运行的容器
   docker ps -a
   # 导出容器
   docker export id > filename.tar
   # 导入容器快照
   cat filename.tar | docker import - ubuntu:v1
   ```

## 3. 镜像操作

1. 镜像列表

   ```python
   docker images 
   或者
   docker image ls
   ```

   

2. 给镜像打标签

   ```python
   docker tag ID xxx:10.0.1
   ```

   

3. 推送镜像到远程

   ```python
   1. 在https://hub.docker.com/ 注册一个账号ilikexie
   2. 创建一个库比如为test
   3. 下载镜像或者制作 hello-world:1.0
   4. 修改镜像标签 docker tag ID ilikexie/test:1.0 
   5. 登录 docker login [docker.io]
   5. 推送：docker push ilikexie/test:1.0
       
       
   例如：
   	推送1.0
       docker tag 14119a10abf4 docker.io/ilikexie/zhu_alpine:1.0
   	docker push docker.io/ilikexie/zhu_alpine:1.0
   	推送2.0
       docker tag 14119a10abf4 docker.io/ilikexie/zhu_alpine:2.0
   	docker push docker.io/ilikexie/zhu_alpine:2.0
        
   ```

   

4.  镜像结构

   ```python
   registry_name/repository_name/image_name:tag_name
   注册名/库名/镜像名：tag名
   比如下载python:
   docker pull docker.io/ilikexie/python:3.6.0
   ```

5. 删除镜像

   ```shell
   # 仅仅删除镜像tag
   docker rmi docker.io/ilikexie/zhu_alpine:1.0 
   # 删除镜像
   docker rmi [-f强制删除] imageId
   
   
   ```

## 4. 容器操作

1. 查看本地的容器进程

   ````shell
   docker ps -a
   # 查看正在运行的容器
   docker ps
   ````

2. 启动容器

   ```shell
   # 开关重启
   docker start/stop/restart 容器id/容器名
   # 启动
   docker run 较为常用
   命令格式：
   	docker run [OPTIONS] IMAGE [COMMAND] [ARG]
   OPRIONS:选项
   -i 表示启动一个可交互的容器
   -t 表示使用终端关联到容器的标准输入输出上
   -d 表示将容器放置后台运行
   --m 退出后删除容器
   --name 表示定义容器唯一名称
   IMAGE 表示要运行的镜像
   COMMOAND 表示运行镜像时要执行的命令
   例如：
   # 启动交互容器
   docker run -it --name my ilikexie/zhu_alpine:2.0
   # 运行结束就删除
   docker run -it --name my2 --rm ilikexie/zhu_alpine:2.0
   # 后台运行
   docker run -d --name my3 ilikexie/zhu_alpine:2.0
   # 执行脚本
   docker run -it --name my4 ilikexie/zhu_alpine:2.0 /bin/echo hello
   ```

   

3. 删除容器

   ```shell
   # 删除停止运行的所有容器
   docker rm `docker ps -a -q`
   # 删除单个容器
   docker rm 容器id/容器名称
   # 强制删除单个容器
   docker rm -f 容器id/容器名称
   ```

4. 进入容器中

   ```shell
   docker exec -it 镜像id /bin/bash
   
   ```

   

​	





