 
## 部署安装脚本
+删除rm  /mysql/data  arch
+ delete from  user where user='';  删除空用户
+ delete from  user where user='';  删除空用户
+ mysql  -uroot  or  -u root -p后面不能加空格 算密码的一部分
##  创建数据库：

> CREATE DATABASE db_name;　　//db_name为数据库名
>GRANT SELECT ON db_name.* TO name;　　　　//给name用户db_name数据库的所有权限
>SHOW processlist;  查看谁在操作
>kill  id 要注意
