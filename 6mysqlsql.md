 
## 部署安装脚本
+删除rm  /mysql/data  arch

## mysql配置多端口
 
cp /etc/my.cnf /etc/my3306.cnf
 
cp /etc/my.cnf /etc/my3307.cnf

+ delete from  user where user='';  删除空用户
+ delete from  user where user='';  删除空用户
+ mysql  -uroot  or  -u root -p后面不能加空格 算密码的一部分



##  创建数据库：

> CREATE DATABAcreate table user(
          
          empno varchar(128),
          ename varchar(128),
          job varchar(128),
            mgr int,
            hiredate timestamp, sal int,  comm int, deptno int
                  )CHARSET=utf8;SE db_name;　　//db_name为数据库名

>GRANT SELECT ON db_name.* TO name;　　　　//给name用户db_name数据库的所有权限
>SHOW processlist;  查看谁在操作
> kill  id 要注意
