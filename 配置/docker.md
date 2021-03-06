### 命令
``` bash
apt install docker.io 		#安装

docker search []			#查找镜像
docker pull []				#下载镜像
docker images				#镜像列表
docker rmi []				#删除镜像

docker run -it [] bash 		#创建并运行
#[-it进入终端,--name 设定容器名称,-v 绑定一个卷]
docker exec -it [] bash		#进入容器，退出时不会停止容器
docker start []				#运行容器
docker stop []				#停止容器
docker rm []				#删除容器
docker ps -a				#显示所有容器

docker stats				#容器运行状态

docker-compose up			#创建并运行
docker-compose start		#运行
docker-compose stop         #停止
```

### 免sudo
```
sudo groupadd docker
sudo gpasswd -a [user] docker
```

### docker-compose.yml示例
```yaml
version: "2"

services:
  db:
    image: mysql:5.6
    # volumes:
    #  - $PWD/db:/var/lib/mysql
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
