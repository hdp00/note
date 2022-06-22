### linux
linux | 说明
-|-
apt install docker.io 		|安装
systemctl enable docker   |自启动
sudo groupadd docker<br>sudo gpasswd -a [user] docker | 免sudo

### docker
docker | 说明
-|-
docker search []			    |查找镜像
docker pull []				    |下载镜像
docker images				      |镜像列表
docker rmi []				      |删除镜像
docker run -it [] bash 		|创建并运行<br>[-it进入终端,--name 设定容器名称,-v 绑定一个卷]
docker exec -it [] bash		|进入容器，退出时不会停止容器<br>[-u user 以user用户进入]
docker start []				    |运行容器
docker stop []				    |停止容器
docker rm []				      |删除容器
docker ps -a				      |显示所有容器
docker stats				      |容器运行状态
docker cp [docker_id]:[docker_file] [system_dir] | 从容器拷贝文件
docker cp [system_file] [docker_id]:[docker_dir]  | 从系统拷贝文件
docker build -t [image:tag] . |构建镜像
docker system df          |查看硬盘
docker system prune       |清理硬盘

### docker-compose
dock-compose | 说明
-|-
docker-compose ps     |列出所有运行容器
docker-compose logs   |查看服务日志输出
docker-compose start  |启动
docker-compose stop   |停止
docker-compose rm     |删除
docker-compose up -d  |构建&启动 [-d 始终运行]
docker-compose down   |关闭&删除

### dockerfile示例
```shell
# django环境，可通过ssh连接
# by hdp 2022.03.19
FROM ubuntu:22.04

WORKDIR /root

COPY acer4741SSH.pub .ssh/authorized_keys
COPY Miniconda3-py39_4.11.0-Linux-x86_64.sh ./

# 安装软件
RUN apt update \  
    && apt install openssh-server -y \
    && apt install nano \
    && apt install git -y \
    # 文件权限和配置
    && chmod 600 .ssh/authorized_keys \
    && chmod 700 .ssh \
    && echo "PasswordAuthentication no" >> /etc/ssh/ssh_config \
    && echo "PubkeyAuthentication yes" >> /etc/ssh/ssh_config 

# miniconda
RUN bash Miniconda3-py39_4.11.0-Linux-x86_64.sh -b \   
    && rm -f Miniconda3-py39_4.11.0-Linux-x86_64.sh

ENV PATH="/root/miniconda3/bin:$PATH"
RUN conda init bash \
    && . ~/.bashrc \
    # 启动环境
    && echo "conda activate django" >> ~/.bashrc \
    && conda create -n django -y \
    && conda activate django \
    && conda install django -y

# 清理
RUN apt purge -y --auto-remove \
    && rm -rf /var/lib/apt/lists/* 

RUN mkdir config
COPY start_service.sh ./config

VOLUME [ "/root/code", "/root/.vscode-server" ]

EXPOSE 22 8000

ENTRYPOINT [ "/root/config/start_service.sh" ]
```

### docker-compose.yml示例
```yaml
version: "2"

services:
  db:
    image: mysql:5.6
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: password
      MYSQL_DATABASE: wordpress
      MYSQL_USER: user
      MYSQL_PASSWORD: password
    volumes:
      - wordpress:/var/www/html

  wordpress:
    depends_on:
      - db
    image: wordpress
    ports:
      - "8001:80"
    restart: always
    environment:
      #指定要使用的数据库名
      WORDPRESS_DB_NAME: wordpress
      #指定要MySQL容器的ip和端口
      WORDPRESS_DB_HOST: db:3306
      #指定登录MySQL的账号
      WORDPRESS_DB_USER: user
      #指定登录MySQL的密码
      WORDPRESS_DB_PASSWORD: password
    volumes:
      - mysql:/var/lib/mysql

volumes:
  wordpress:
  mysql:
```

```yaml
version: '2'

services:
  db:
    image: mariadb
    restart: always
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW --skip-innodb-read-only-compressed
    environment:
      - MYSQL_ROOT_PASSWORD=password
      - MYSQL_PASSWORD=password
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=user
    volumes:
      - /home/user/mysql:/var/lib/mysql

  app:  
    image: nextcloud
    restart: always
    ports:
      - 8003:80
    links:
      - db  
    environment:
      - MYSQL_PASSWORD=password
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=user
      - MYSQL_HOST=db
    volumes:
      - /home/user/nextcloud:/var/www/html

```