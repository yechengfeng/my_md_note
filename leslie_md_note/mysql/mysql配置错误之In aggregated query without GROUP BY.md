**问题描述**

* *关于java在调用mysql的时候报错*

     ```
Error querying database.  Cause: com.mysql.jdbc.exceptions.jdbc4.MySQLSyntaxErrorException: In aggregated query without GROUP BY,expression #2 of SELECT list contains nonaggregated column 'pay.t.type'; this is incompatible with sql_mode=only_full_group_by
     ```



* **错误原因**

  在MySQL5.7.5后，默认开启了ONLY_FULL_GROUP_BY，所以导致了之前的一些SQL无法正常执行，其实，是我们的SQL不规范造成的，因为group by 之后，返回的一些数据是不确定的，所以才会出现这个错误。

* **解决方案**

​       windows下 修改 My.int  文件，linux下修改my.cnf 文件

1.  找到sql-mode的位置，去掉ONLY_FULL_GROUP_BY，没有的需要在 **[mysqld]**下加上

    		

   ```
   sql-mode =
   STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION
   ```

   

2. 重启数据库

   1. sudo service mysql restart 

       *或者*

   2.  sudo systemctl restart mysqld

3. 登录mysql  

   查看  *show variables like '%sql_mode**’**;*



[参考](https://blog.csdn.net/qq_26365837/article/details/88020755)

