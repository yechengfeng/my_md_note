###  mysql 存特殊字符，如表情符号等。默认的uft-8或者gbk是不支持的。



  **utf-8 和 utf8mb4。utf-8mb4 可以接受特殊字符， 此命令查看现在的字符集**

```mysql
SHOW VARIABLES WHERE Variable_name LIKE 'character_set_%' OR Variable_name LIKE 'collation%'; 


```

1. 修改 my.cnf文件

   ```properties
   [client]
   default-character-set=utf8mb4
   [mysql]
   default-character-set=utf8mb4
   [mysqld]
   character-set-client-handshake = FALSE
   character-set-server=utf8mb4
   collation-server = utf8mb4_unicode_ci
   init_connect='SET NAMES utf8mb4'
   ```

2. 重启 数据库   

   ```shell
   sudo systemctl restart mysqld
   ```

   

3. 再次查看 字符编码

   

4. 对具体的表进行编码设置

   ```mysql
   修改表的编码：
   alter table table_name default character set utf8mb4 collate=utf8mb4_general_ci;
   
   修改字段的编码：
   ALTER TABLE table_name convert to CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
   
    
   ```

   

​	 