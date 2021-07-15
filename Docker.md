# Docker 学习笔记

## 安装 Docker

> curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun

## 安装 esp-idf 镜像

> docker pull espressif/idf:latest

## Docker 配置

需要将 Docker 加入用户组，省略命令前面的 sudo，[参考链接](https://murphypei.github.io/blog/2018/12/docker-add-group)

1. 检查是否存在 docker 分组

   > sudo cat /etc/group | grep docker

   若不存在，则执行

   > sudo groupadd docker 

   创建分组

2. 将用户添加至 docker 分组

   > sudo usermod -aG docker <usrname>

   其中 `-G` 表示下一参数为 group 名，`-a` 表示把 `username` 添加到前一参数的 gorup 中

3. 修改守护进程绑定的套接字的权限，能够被docker分组访问

   > sudo chmod a+rw /var/run/docker.sock

   其中 `a` 表示所有用户，`+` 表示添加权限，`rw` 表示读写权限，[参考链接1](http://www.gnu.org/software/coreutils/manual/html_node/Setting-Permissions.html#Setting-Permissions)/[参考链接2](https://www.runoob.com/linux/linux-comm-chmod.html)

4. 退出当前用户登陆状态，然后重新登陆，以便让权限生效

   > sudo systemctl restart docker

5. 确认可直接运行 docker 命令

   > docker info

## Docker 指令

1. 启动容器

   > docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
   >
   > 常用 Options : 
   >
   > ​	-i：interactive，交互操作
   >
   > ​	-t：终端
   >
   > ​	--rm：退出容器后自动删除容器
   >
   > ​	-v \$PWD:/project：把宿主系统的当前目录 (\$PWD) 挂载到 Docker 容器的 /project 目录下
   >
   > ​	-w /project：开启容器后自动进入 /project 目录下
   >
   > ​	--device=/dev/ttyUSB0：把宿主系统的 USB 设备映射进 docker 容器中
   >
   > 典型命令：
   >
   > docker run --device=/dev/ttyUSB0 --rm -v $PWD:/project -w /project -it espressif/idf:release-v4.1

   进入容器后命令前显示井号

2. 退出容器

   > \# exit
   >
   > 或 ctrl+D

3. 显示所有容器

   > docker ps -a

   去掉 -a 选项即显示所有正在运行的容器

4. 启动一个已停止的容器

   > docker start <CONTAINER ID>

   其中 CONTAINER ID 可由 `ps` 指令获得

5. 停止运行中的容器

   > docker stop <CONTAINER ID>

6. 进入容器

   > docker attach <CONTAINER ID>

   > docker exec <CONTAINER ID> <command>

   前提为对应容器正在运行

   attach 命令进入容器内，退出时容器停止运行；exec 命令使容器运行 `command` 中的指令并打印，运行结束后自动回到宿主系统

7. 删除容器

   > docker rm <CONTAINER ID>

8. 显示某容器日志

   > docker logs <CONTAINER ID>

   > docker logs <CONTAINER NAME>

   容器状态可为运行中或停止状态，CONTAINER NAME 可由 `ps` 指令获得

9. 显示所有镜像

   > docker images

10. 删除某一镜像文件

    > docker rmi <REPOSITORY>:<TAG>

    > docker rmi <IMAGE ID>

    其中 `IMAGE ID` 可通过 `images` 指令获得 

11. 设置镜像标签

    > docker tag <IMAGE ID> <REPOSITORY>:<new tag> 