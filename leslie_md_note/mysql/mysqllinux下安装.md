一 。找到对应的版本

\1.  mysql 历史版本 tar 包 地址 https://downloads.mysql.com/archives/community/ 

\2.  mysql最新版本  rpm包 

https://dev.mysql.com/downloads/repo/yum/ 

\3. mysql历史版本 ： https://repo.mysql.com/  

1. 获取 相关的版本 拼接url。

https://dev.mysql.com/get/

二 。下载

 （wget常用参数）	https://www.cnblogs.com/mike168/p/11355420.html

wget  urls

三 。rpm方式下载

​	（rpm常用参数） https://www.cnblogs.com/luwikes/archive/2011/09/14/2176575.html

了解rpm包管理。

\1. 检查rpm管理的安装包是否安装有 mysql。

```
rpm -qa | grep mysql
```

\2. 如果有卸载 

```
rpm -e mysql  普通删除
rpm -e --nodeps mysql　　// 强力删除模式，如果使用上面命令删除时，提示有依赖的其它文件，则用该命令可以对其进行强力删除
```

四，安装  

(https://blog.csdn.net/wanyefu/article/details/81026936)

（https://www.cnblogs.com/dengshihuang/p/8029092.html）

（https://www.cnblogs.com/zhangkaimin/p/4171269.html）

yum -y install mysql57-community-release-el7-10.noarch.rpm

yum install -y mysql-server mysql mysql-deve

rpm -qi mysql-community-server

systemctl start mysqld.service

systemctl status mysqld.service

grep "password" /var/log/mysqld.log //查看root原始密码

mysql -u root -p

ALTER USER 'root'@'localhost' IDENTIFIED BY 'new password';