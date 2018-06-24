##  聚合函数
> where  xx=1  having  sum(xxx)>100;
```
select ename, salary, 
       case
        when salary > 1 and salary <= 1000 then 'LOWER'
        when salary > 1000 and salary <= 2000 then 'MIDDLE'
        when salary > 2000 and salary <= 4000 then 'HIGH'
        else 'HIGHEST'
       end
from   ruozedata_emp4;



```


join
create table  a (id  int,name string)
row  format  delimited fields  terminated by '\t';
create table  b (id  int,age int)
row  format  delimited fields  terminated by '\t';


插入的数据 用tab键  隔开  隔开！！！！

load data local inpath '/home/hadoop/data/1.txt' overwrite into table a;



### 分区表


静态分区

alter table PARTITIONS convert to character set latin1;
alter table PARTITION_KEYS convert to character set latin1;


在ruozedata下建立了分区表 用fs  -ls 查看不到分区文件 怎么办怎么办(表数据不对 或者hive没退出)
索性不用ruozedata 另外创建！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！
nonono

只有  where event_month='2014-05'; （如果是分区查询一定要带上分区的条件）

用fs  -ls 才能那查看分区文件
> 动态分区
```
create table ruozedata_emp 
(empno int, ename string, job string, mgr int, hiredate string, salary double, comm double, deptno int)
ROW FORMAT DELIMITED 

FIELDS TERMINATED BY '\t' ;


LOAD DATA LOCAL INPATH '/home/hadoop/data/emp.txt' OVERWRITE INTO TABLE ruozedata_emp; 

[hadoop@hadoop001 data]$ hadoop fs -ls /user/hive/warehouse/ruozedata.db/order_partition
18/06/23 12:56:31 WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
Found 1 items
drwxr-xr-x   - hadoop supergroup          0 2018-06-23 12:52 /user/hive/warehouse/ruozedata.db/order_partition/event_month=2014-05
[hadoop@hadoop001 data]$ hadoop fs -ls /user/hive/warehouse/ruozedata.db/order_partition/event_month=2014-05
18/06/23 12:56:47 WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
Found 1 items
-rwxr-xr-x   1 hadoop supergroup        700 2018-06-23 12:52 /user/hive/warehouse/ruozedata.db/order_partition/event_month=2014-05/emp.txt
[hadoop@hadoop001 data]$ hadoop  fs -mkdir /user/hive/warehouse/ruozedata.db/order_partition/event_month=2014-06
18/06/23 12:57:45 WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
[hadoop@hadoop001 data]$ hadoop  fs -put emp.txt /user/hive/warehouse/ruozedata.db/order_partition/event_month=2014-06
18/06/23 12:58:02 WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
[hadoop@hadoop001 data]$ hadoop  fs -ls /user/hive/warehouse/ruozedata.db/order_partition/event_month=2014-06         
18/06/23 12:58:35 WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
Found 1 items
-rw-r--r--   1 hadoop supergroup        700 2018-06-23 12:58 /user/hive/warehouse/ruozedata.db/order_partition/event_month=2014-06/emp.txt
动态分区明确要求：分区字段写在select的最后面	
insert into table ruozedata_dynamic_emp partition(deptno)
select empno,ename,job,mgr,hiredate,salary,comm,deptno from ruozedata_emp ;
	
	
	
set hive.exec.dynamic.partition.mode=nonstrict;



这是hive中常用的设置key=value的方式
语法格式： 
	set key=value; 设置	
	set key;       取值

	select *from ruozedata_dynamic_emp;



```

## insert 模式





多级分区 了解下
多级分区
create table order_mulit_partition(
ordernumber string,
eventtime string
)
partitioned by (event_month string,event_day string)
row format delimited fields terminated by '\t';

LOAD DATA LOCAL INPATH '/home/hadoop/data/order.txt' 
OVERWRITE INTO TABLE order_mulit_partition 
PARTITION(event_month='2014-05', event_day='01'); 
