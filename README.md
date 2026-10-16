# docker镜像网站
hub.docker.com

# 下载镜像
docker pull docker.io/library/nginx:latest
docker.io: 仓库地址
library: 命令空间/作者名
nginx: 镜像名
latest: 版本号

# 配置镜像站
sudo vim /etc/docker/daemon.json
将镜像加速地址写入
{
  "registry-mirrors": [
    "https://docker.m.daocloud.io",
    "https://dockerproxy.com",
    "https://docker.nju.edu.cn",
    "https://mirror.baidubce.com"
  ]
}

重启docker服务
sudo service docker restart

# 查看下载的镜像
sudo docker images

# 删除镜像
sudo docker rmi "镜像名"

# 启动容器
sudo docker run -d "镜像名"

# 查看镜像进程
sudo docker ps

# 端口映射
sudo docker run -p 80:80 "镜像名" 
80:80 == 宿主机端口:容器端口

# 挂载区 （绑定挂载）
sudo docker run -d -p 8090:80 -v /website/html:/usr/share/nginx/html "镜像名"

# 挂载 - 创建一个存储空间（命名卷）
sudo docker volume create nginx_html
sudo docker run -d -p 8090:90 -v nginx_html:/usr/share/nginx/html "镜像名"

# 查看挂载卷存放位置
sudo docker volume inspect nginx_html

# 传递变量
sudo docker run -d -e 变量名=赋值 nginx

# 打开容器并运行 /bin/bash
sudo docker run -it /bin/bash

# 容器停止便立即重启
sudo docker run -d --restart always nginx
sudo docker run -d --restart unless-stopped nginx （手动停止的容器不会自动重启）

# 进入一个正在运行的容器
docker exec -it nginx /bin/sh

# 创建镜像
docker build -t docker_test .