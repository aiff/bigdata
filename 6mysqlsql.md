 
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
 insert into emp  values(736	,'SMITH',	'CLERK'	 ,  7902	 ,   '1980-12-17'	 , 800.00	,null,	20);
 insert into emp  values(7499,	'ALLEN',	'SALESMAN'	,7698,	'1981-2-20'	,1600.00,	300.00,30);

>GRANT SELECT ON db_name.* TO name;　　　　//给name用户db_name数据库的所有权限
>SHOW processlist;  查看谁在操作
> kill  id 要注意



````

a.表名称 字段名称 不能是中文 不能是汉语拼音 
b.统一风格： 已经存在的表 风格是什么==>leader check
		create_user
		createuser
	    新项目 风格是什么 ==》 by you

	    ctime
	    cretime
	    createtime
	    cre_time
	    create_time

c.第一个字段 必然是 id 自增长 主键 无意义  (懂不懂mysql)

d.一张表只有一个主键 primary key==》id
     unique+not null

     业务字段 比如需要唯一  unique约束

     ALTER TABLE ruozedata.rzdata 
     ADD CONSTRAINT rzdata_un UNIQUE KEY (name) ;

````
