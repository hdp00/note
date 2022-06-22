[TOC]

# Linux配置

## adduser
```
adduser name

#获取root权限
nano /etc/sudoers
在“root ALL=(ALL:ALL) ALL”下面加入
name ALL=(ALL:ALL) ALL
```

## SSH
```
//创建秘钥
ssh-keygen
//将公钥添加到系统
cd /home/[user]/.ssh
cat [key].pub >> authorized_keys 

关闭ssh密码登录
修改配置文件/etc/ssh/sshd_config
PasswordAuthentication no
//重启
service sshd restart


```
```
之后需要配置.ssh/config
Host 别名
    Hostname 主机名
    Port 端口
    User 用户名
    IdentityFile ./sshFile
```
```
//登录
ssh username@192.168.1.103
or
ssh 别名
```

## Apache
```
#安装
sudo apt install apache2
#重启
service apache2 restart
```
```
/ect/Apache2目录下
1. "apache2.conf"文件，获取访问权限，将"Require all denied"修改成"Require all granted".
2. "sites-avaibled"中的"000-default.conf"，修改网站目录"DocumentRoot /var/www/html".
```

## MySQL
```
#安装
sudo apt install mysql-server
sudo apt install mysql-client
sudo apt install libmysqlclient-dev
sudo apt install mysql-workbench
```
```
#创建用户
grant all privileges on *.* to username@localhost identified by 'password';
#更新授权表
flush privileges;
```

## nginx

### command
> - 安装 ```sudo apt-get install nginx```
> - 启动 ```/etc/init.d/nginx start```
> - 关闭 ```/etc/init.d/nginx stop```
> - 重启 ```/etc/init.d/nginx restart```
> - 删除apache2 ```sudo apt-get --purge remove apache2```

### config
> 在/etc/nginx/conf.d目录新建一个default.conf文件，内容如下：
```
server {
    listen       8001;   #配置监听端口
    server_name  localhost;  #配置域名
    #charset koi8-r;     
    #access_log  /var/log/nginx/host.access.log  main;
    location / {
        #root   /usr/share/nginx/html;     #服务默认启动目录
        #index  index.html index.htm;    #默认访问文件
        include uwsgi_params;
        uwsgi_pass 127.0.0.1:9000;
        uwsgi_read_timeout 2;
    }

    error_page   500 502 503 504  /50x.html;   #错误状态码的显示页面，配置后需要重启
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    location ~ .*\.(htm|html)$ {
        expires off;    #关闭缓存
    }
}

```


## squid

```
//安装
apt install squid
//安装密码生成工具
apt install apache2-utils
//生成密码文件
htpasswd  -c /etc/squid/passwd proxy_username
//启动
/etc/init.d/squid start
```

配置文件```/etc/squid/squid.conf```
```
//无密码配置
http_access deny all改为 http_access allow all

//密码配置，注意要将http_access deny all放最后
http_port 3128

auth_param basic program /usr/lib/squid/basic_ncsa_auth /etc/squid/passwd
acl auth_user proxy_auth REQUIRED
http_access allow auth_user

http_access deny all
```

test
```
//http方式
export http_proxy=http://45.40.206.58:3128
curl http://www.baidu.com

//https方式
export https_proxy=http://192.168.163.117:3128
curl https://www.baidu.com

//如果网络是通过http代理服务器出去的，而代理服务器需要用户名和密码，那么输入：
curl -U proxyuser:proxypassword http://www.baidu.com
```

## 一些指令
``` sh
#查看python进程
ps aux |grep python

#scp
#上传下载文件
scp /path/filename username@servername:/path/
scp username@servername:/path/filename /var/www/local_dir
#上传下载目录
scp -r username@servername:/var/www/remote_dir/（远程目录） /var/www/local_dir（本地目录）
scp -r local_dir username@servername:remote_dir

#查看nginx网络状态
netstat  -anptu |grep nginx

修改用户组
如果要修改该目录下所有文件和目录，使用-R参数。
chgrp -R [group] [file]
修改文件所有者
chown [user] [file]
```









