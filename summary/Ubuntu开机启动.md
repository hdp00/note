update-rc.d增加开机启动服务
给Ubuntu添加一个开机启动脚本，操作如下：
1、新建个脚本文件new_service.sh
```
#!/bin/bash
# command content
```
  
exit 0
2、设置权限
```
sudo chmod 755 new_service.sh
#或者
sudo chmod +x new_service.sh
```
3、把脚本放置到启动目录下
sudo mv new_service.sh /etc/init.d/
4、将脚本添加到启动脚本
执行如下指令，在这里90表明一个优先级，越高表示执行的越晚
cd /etc/init.d/
sudo update-rc.d new_service.sh defaults 90
5、移除Ubuntu开机脚本
sudo update-rc.d -f new_service.sh remove
6、通过sysv-rc-conf来管理上面启动服务的启动级别等，还是开机不启动
sudo sysv-rc-conf 
7、update-rc.d的详细参数
使用update-rc.d命令需要指定脚本名称和一些参数，它的格式看起来是这样的（需要在 root 权限下）：
update-rc.d [-n] [-f] <basename> remove
update-rc.d [-n] <basename> defaults
update-rc.d [-n] <basename> disable|enable [S|2|3|4|5]
update-rc.d <basename> start|stop <NN> <runlevels>
-n: not really
-f: force
其中：
disable|enable：代表脚本还在/etc/init.d中，并设置当前状态是手动启动还是自动启动。
start|stop：代表脚本还在/etc/init.d中，开机，并设置当前状态是开始运行还是停止运行。（启用后可配置开始运行与否）
NN：是一个决定启动顺序的两位数字值。（例如90大于80，因此80对应的脚本先启动或先停止）
runlevels：则指定了运行级别。
实例：
（1）、添加一个新的启动脚本sample_init_script，并且指定为默认启动顺序、默认运行级别（还记得前面说的吗，首先要有实际的文件存在于/etc/init.d，即若文件/etc/init.d/sample_init_script不存在，则该命令不会执行）：
update-rc.d sample_init_script defaults
上一条命令等效于（中间是一个英文句点符号）：
update-rc.d sample_init_script start 20 2 3 4 5 . stop 20 0 1 6
（2）、安装一个启动脚本sample_init_script，指定默认运行级别，但启动顺序为50：
update-rc.d sample_init_script defaults 50
（3）、安装两个启动脚本A、B，让A先于B启动，后于B停止：
update-rc.d A 10 40
update-rc.d B 20 30
（4）、删除一个启动脚本sample_init_script，如果脚本不存在则直接跳过：
update-rc.d -f sample_init_script remove
这一条命令实际上做的就是一一删除所有位于/etc/rcX.d目录下指向/etc/init.d中sample_init_script的链接（可能存在多个链接文件），update-rc.d只不过简化了这一步骤。
（5）禁止Apache/MySQL相关组件开机自启：
update-rc.d -f apache2 remove
update-rc.d -f mysql remove
8、服务的启动停止状态
```
#通过service，比如
sudo service xxx status
sudo service xxx start
sudo service xxx stop
sudo service xxx restart
```
9、查看全部服务列表
sudo service --status-all
