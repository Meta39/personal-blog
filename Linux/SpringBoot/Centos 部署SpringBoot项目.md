```shell
# 查看PID和端口占用情况
netstat -ntlp
# 查看某个端口是否被占用
netstat -anp |grep 端口号
# 查询java端口占用
ps -aux | grep java
# 查询运行内存（res）占用
top -p 应用的PID
# 杀死占用端口
kill -9 应用的PID
```
linux开放端口（开放完端口要重启防火墙）
```shell
# 命令含义：
# --zone #作用域
# --add-port=8080/tcp  #添加端口，格式为：端口/通讯协议
# --permanent  #永久生效，没有此参数重启后失效
firewall-cmd --zone=public --add-port=8080/tcp --permanent
# 重启防火墙
firewall-cmd --reload
# 查看开放的端口列表
firewall-cmd --zone=public --list-ports
```
---
创建.sh启动脚本（sh的文件，windows复制粘贴到linux可能会报错，dos要format成unix执行。）
```shell
vim xxx/xxx.sh
```
```shell
#!/bin/sh
#注意：在sh文件中=赋值，左右两侧不能有空格
APP_NAME="Demo.jar"
command=$1

# 启动
function start(){
	kills
    rm -f pid
    nohup java -jar ${APP_NAME} >/dev/null 2>&1 &
    echo $! > pid
    check
}

# 检查项目是否正常运行
function check(){
    pid=`ps -ef|grep $APP_NAME|grep -v grep|grep -v kill|awk '{print $2}'`
    if [ ${pid} ]; then
        echo 'App is running.'
    else
        echo 'App is NOT running.'
    fi
}

# 强制kill进程
function kills(){
    pid=`ps -ef|grep $APP_NAME|grep -v grep|grep -v kill|awk '{print $2}'`
    if [ ${pid} ]; then
        echo 'Kill Success!'
        kill -9 $pid
    fi
}

# 输出进程号
function pid(){
    pid=`ps -ef|grep $APP_NAME|grep -v grep|grep -v kill|awk '{print $2}'`
    if [ ${pid} ]; then
        echo 'process '$APP_NAME' pid is '$pid
    else
        echo 'process '$APP_NAME' is not running.'
    fi
}

if [ "${command}" ==  "start" ]; then
    start
elif [ "${command}" ==  "check" ]; then
     check
elif [ "${command}" ==  "kill" ]; then
     kills
elif [ "${command}" == "pid" ]; then
     pid
else
    echo "Unknow argument...."
fi
```
使用脚本
```shell
./xxx.sh start
```
---
新增用户
```shell
# -m 自动建立用户的登入目录 -d<登入目录>：指定用户登入时的启始目录
sudo useradd fu -m -d /home/fu
# 将用户添加进工作组（wheel是组名，xieyun是用户名）
usermod -G wheel fu
# 修改密码
passwd fu
# 切换用户
su fu
# 查看组
groups fu
# 删除用户
userdel xxx
```