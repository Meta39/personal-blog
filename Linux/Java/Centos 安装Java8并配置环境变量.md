```shell
xxx.noarch不用删
[x@x /]$ rpm -qa|grep java
java-1.8.0-openjdk-headless-1.8.0.322.b06-1.el7_9.x86_64
javapackages-tools-3.4.1-11.el7.noarch
python-javapackages-3.4.1-11.el7.noarch
tzdata-java-2021e-1.el7.noarch
java-1.7.0-openjdk-headless-1.7.0.261-2.6.22.2.el7_8.x86_64
java-1.7.0-openjdk-1.7.0.261-2.6.22.2.el7_8.x86_64
java-1.8.0-openjdk-1.8.0.322.b06-1.el7_9.x86_64

[x@x /]$ rpm -e --nodeps 查询到的jdk

创建存放目录
[x@x /]$ mkdir /usr/local/java

进入存放目录
[x@x /]$ cd /usr/local/java

解压jdk
[x@x java]$ tar -zxvf jdk-1.8.0-linux-x64.tar.gz

[x@x java]$ vi  /etc/profile
```

> 找到export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE HISTCONTROL，在下面写上：

```shell
#set java environment
export JAVA_HOME=/usr/local/java/jdk1.8.0_291
export CLASSPATH=.:$JAVA_HOME/lib
export PATH=$PATH:$JAVA_HOME/bin:$JAVA_HOME/jre/bin
```

> :wq  保存退出，最后使用source /etc/profile是文件生效。

```shell
[root@x ~]# source /etc/profile
[root@x ~]# java -version
java version "1.8.0_291"
Java(TM) SE Runtime Environment (build 1.8.0_291-b10)
Java HotSpot(TM) 64-Bit Server VM (build 25.291-b10, mixed mode)
```
