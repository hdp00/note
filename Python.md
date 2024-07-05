[TOC]

## Django

### command
> - 创建项目 ```django-admin startproject mysite```
> - 运行 ```python manage.py runserver```
> - 创建应用 ```python manage.py startapp books```
> - 生成数据库定义 ```python manage.py makemigrations books```
> - 生成数据库 ```python manage.py migrate```
> - 创建管理员 ```python manage.py createsuperuser```
> - 收集静态文件 ```python manage.py collectstatic```

### settings.py
```
# 设置时区
TIME_ZONE = 'Asia/Shanghai'
# 注释此代码，可避免Forbidden (CSRF cookie not set.)错误
django.middleware.csrf.CsrfViewMiddleware
# 添加应用
INSTALLED_APPS = [
    'books',
]
```

### others

#### 远程访问开发者模式
```
//command 监听所有IP
python3 manage.py runserver 0.0.0.0:8000
//settings.py 设置允许访问的域名
ALLOWED_HOSTS = ['192.168.43.128']
```

#### VSCode
```
//debug
必须加上"--noreload"选项，否则无法调试
//python目录设置
python.pythonpath python.venvpath
```

格式化代码
```
//command
pip install yapf
<//settings.json>
{
    "python.formatting.provider": "yapf",//配置
    //格式设置
    "python.formatting.yapfArgs": [
        "--style", "{BLANK_LINES_AROUND_TOP_LEVEL_DEFINITION: 1}"//类之间空行为1
     ]
}
//快捷键
Ctrl + Shift + I
```
---

## uwsgi

### command
> - 安装 ```conda install uwsgi``` or ```python3 -m pip install uwsgi```
> - 以配置文件运行 ```uwsgi --ini mysite_uwsgi.ini```

### test
创建测试文件
```
def application(env, start_response):
    start_response('200 OK', [('Content-Type','text/html')])
    return [b"Hello World"]
```
运行测试文件
```
uwsgi --http :9000 --wsgi-file test.py
```

### config
配置文件,放在/home/hdp/code/django/mysite
```
[uwsgi]
;浏览器调用
http=9000
;nginx调用
;socket=:9000 
chdir=/home/hdp/code/django/mysite
master=true
processes=4
vacuum=true
;于myweb_uwsgi.ini文件来说，与它的平级的有一个myweb目录，这个目录下有一个wsgi.py文件
module = mysite.wsgi
;pythonpath=/home/hdp/anaconda3/bin/python
```

### question
- no internal routing support, rebuild with pcre support
```
pip uninstall uwsgi
sudo apt-get install libpcre3 libpcre3-dev
pip install uwsgi --no-cache-dir
```


## conda
### 安装
```
可在https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/查找版本
//下载
wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/Anaconda3-5.3.1-Linux-x86_64.sh
```

### command
> - 查看帮助信息 ```conda -h```

> - 创建新环境 ```conda create --name <env_name>```
> - 切换环境 ```source activate <env_name>```
> - 退出环境 ```source deactivate```
> - 显示已创建环境 ```conda env list```
> - 复制环境 ```conda create --name <new_env_name> --clone <copied_env_name>```
> - 删除环境 ```conda remove --name <env_name> --all```

> - 安装包 ```conda install <package_name>```
> - 卸载包 ```conda remove <package_name>```
> - 更新所有包 ```conda update --all```
> - 更新包 ```conda update <package_name>```
> - 基本升级 ```conda update conda```

> - 删除没有用的包 ```conda clean -p```
> - 删除tar包 ```conda clean -t```
> - 删除所有的安装包及cache ```conda clean -y -all```


## PyQt5 
```
安装
sudo apt-get install qt5-default qttools5-dev-tools
sudo apt-get insatll python3-pyqt5
```

---
