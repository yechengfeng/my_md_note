[centos7 查看开机启动项和程序服务](https://www.cnblogs.com/MUQINGFENG123/p/11532751.html)

* systemctl list-unit-files  (查看开机启动项)

* systemctl list-unit-files  |  grep 程序名称  （查看某些服务开机启动状态）

* systemctl  list-unit-files |  grep enable （查看哪些为开机启动服务）

