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


在ruozedata下建立了分区表 用fs  -ls 查看不到分区文件 怎么办怎么办
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

