> 以管理员的身份运行cmd(重点)
进入到MySQL8.0.23的bin目录。如：==cd D:\software\mysql-8.0.23-winx64\bin

#### 安装
```shell
mysqld --initialize-insecure --user=mysql
mysqld --install
net start mysql
#登录mysql。初始密码为空，直接回车即可
mysql -uroot -p
```
cmd登录后执行的SQL语句
```mysql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '123456' PASSWORD EXPIRE NEVER;
#必须刷新
FLUSH PRIVILEGES;
```

---
> 新建用户并修改加密方式，如：创建x用户密码为123456及修改加密方式
```mysql
CREATE USER 'x'@'%' IDENTIFIED WITH mysql_native_password BY 'x' PASSWORD EXPIRE NEVER;
# 授权，WITH GRANT OPTION表示可以给其它人授权
GRANT all on *.* to 'x'@'%' WITH GRANT OPTION;
# 刷新（必须）
FLUSH PRIVILEGES;
```