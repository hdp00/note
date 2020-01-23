``` bash
#安装
#java
sudo apt-get install openjdk-8-jdk
java –version

sudo apt install python3-pip


sudo apt-get install mysql-server mysql-client
sudo pip3 install pymysql
sudo pip3 show mysqlclient

#flask
sudo pip3 install flask

#docker
$ sudo apt-get update
$ sudo apt-get install docker.io
$ sudo ln -sf /usr/bin/docker.io /usr/local/bin/docker
$ sudo sed -i '$acomplete -F _docker docker' /etc/bash_completion.d/docker.io

$ curl -sSL https://get.docker.io/ubuntu/ | sudo sh


免sudo
sudo groupadd docker
sudo gpasswd -a ${USER} docker
docker时间同步：
可以通过docker cp /etc/localtime [containerId]:/etc/localtime进行修改


docker 指令
数据卷
docker run -v /home/hdp/code/python/:/code --name data ubuntu:flask
运行
docker run -ti  --volumes-from data --name hdp -p 5000:5000 ubuntu:flask /bin/bash 
进入
docker exec -ti hdp bash


```