
>  打开debug模式可以看到点信息  没不要不要开
hive -hiveconf hive.root.logger=DEBUG,console



>   从外导入一个文件
  
LOAD DATA LOCAL INPATH '/home/hadoop/app/hadoop-2.6.0-cdh5.7.0/demo.txt' OVERWRITE INTO TABLE ruozedata_emp; 
local: 从本地文件系统加载数据到hive表
非local：从HDFS文件系统加载数据到hive表


##Failed with exception Unable to alter table. For direct MetaStore DB connections, we don't support retries at the client level.
FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.MoveTask


alter database hive character set latin1;

#  导入的时候不要复制语句进去  要写好再传过去  空格不会很好的处理掉

都不清楚什么时导入成功了 
```


 >
    > LOAD DATA LOCAL INPATH '/home/hadoop/app/hadoop-2.6.0-cdh5.7.0/demo.txt' O                                                                                                                                                            
    VERWRITE INTO TABLE ruozedata_emp2;
Loading data to table default.ruozedata_emp2
Warning: fs.defaultFS is not set when running "chgrp" command.
Warning: fs.defaultFS is not set when running "chmod" command.
Failed with exception Unable to alter table. For direct MetaStore DB connections                                                                                                                                                           
, we don't support retries at the client level.
FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.MoveT                                                                                                                                                           
ask
hive> show databases;
OK
default
ruozedata
Time taken: 0.03 seconds, Fetched: 2 row(s)
hive> use
    > ruozedata
    > use ruozedata
    > ;
FAILED: ParseException line 3:0 missing EOF at 'use' near 'ruozedata'
hive> use ruozedata;
OK
Time taken: 0.014 seconds


 首先我们看到了 一个提示 unable to alter table 再往上看
  Warning: fs.defaultFS is not set when running "chgrp" command.
Warning: fs.defaultFS is not set when running "chmod" command.
因为没有配置好>fs.defaultFS 
 
 处理：  修改你的  core-site.xml 
 <property>
    <name>fs.defaultFS</name>
    <value>hdfs://hadoop:9000</value>
    <description>NameNode的URI</description>
  </property>
  <property>

````




### DDL：Data Defination Language 
	描述Hive表数据的结构：create alter drop.....
	
	Hive构建在Hadoop之上
		Hive的数据存放在HDFS之上
		Hive的元数据可以存放在RDBMS之上
	
	Database/Table

## CREATE (DATABASE|SCHEMA) [IF NOT EXISTS] database_name
  [COMMENT database_comment]
  [LOCATION hdfs_path]
  [WITH DBPROPERTIES (property_name=property_value, ...)];
  
default是Hive中默认的一个数据库 
	/user/hive/warehouse/
	
create database hive;

/user/hive/warehouse/<databasename>.db


DROP (DATABASE|SCHEMA) [IF EXISTS] database_name [RESTRICT|CASCADE];

create  alter drop show desc use
	
	
基本数据类型	
	疯！！！！！！！！！！！！！！
	int bigint  float  double  decimal
	boolean         XXX
	string
	date/timestamp  XXX
		
分隔符 
	行: \n
	列: \001 ^A  ==>   
		1	zhangsan	30
		1$$$zhangsan$$$30
	map/struct/array


##建立普通表
CREATE TABLE aaa
(id int comment 'this is id', name string comment 'this id name' )
comment 'this is ruozedata_person'
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY '\t' ;





CREATE TABLE part
(orfer  string comment 'this is id', every string comment 'this id name' )
partition   
comment 'this is ruozedata_person'
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY '\t' 





	
Table
use ruozedata;
CREATE TABLE demo11
(id int comment 'this is id', name string comment 'this id name' )
comment 'this is ruozedata_person'
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY '\t' ;

create table ruozedata_emp 
(empno int, ename string, job string, mgr int, hiredate string, salary double, comm double, deptno int)
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY '\t' ;
 
LOAD DATA LOCAL INPATH '/home/hadoop/data/emp.txt' OVERWRITE INTO TABLE ruozedata_emp; 
local: 从本地文件系统加载数据到hive表
非local：从HDFS文件系统加载数据到hive表

OVERWRITE: 加载数据到表的时候数据的处理方式，覆盖
非OVERWRITE：追加

##  CTAS
CREATE table ruozedata_emp2 as select * from ruozedata_emp;
>   可以到网页上观看   1287.0.0.1:8088/cluster/aps 任务
CREATE table ruozedata_emp3 like ruozedata_emp;

ALTER TABLE ruozedata_emp3 RENAME TO ruozedata_emp3_new;

create alter drop show desc 

# 创建表默认使用的是MANAGED_TABLE：内部表
	ruozedata_emp_managed
	drop：hdfs+meta
	
# EXTERNAL：外部表 删除后 还有留底
create EXTERNAL table ruozedata_emp_external 
(empno int, ename string, job string, mgr int, hiredate string, salary double, comm double, deptno int)
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY '\t'
LOCATION "/ruozedata/external/emp" ;
	drop: drop meta
 
hdfs://hadoop000:8020/ddddd
s3a://xxx/yyyy 
s3n
### create table ruozedata_emp4 as select  *from ruozedata_emp;
create table ruozedata_emp4 like ruozedata_emp;

INSERT OVERWRITE TABLE ruozedata_emp4
select * FROM ruozedata_emp;
 
INSERT INTO TABLE ruozedata_emp4
SELECT empno,job, ename,mgr, hiredate, salary, comm, deptno from ruozedata_emp;
 
## 重跑：解决不了幂等 ***** 
log
	2055  ==> 20
	2054  ==> 20
	....  
	1959  ==> 19
 
CREATE [TEMPORARY] [EXTERNAL] TABLE [IF NOT EXISTS] [db_name.]table_name    -- (Note: TEMPORARY available in Hive 0.14.0 and later)
  [(col_name data_type [COMMENT col_comment], ... [constraint_specification])]
  [COMMENT table_comment]
  [PARTITIONED BY (col_name data_type [COMMENT col_comment], ...)]
  [CLUSTERED BY (col_name, col_name, ...) [SORTED BY (col_name [ASC|DESC], ...)] INTO num_buckets BUCKETS]
  [SKEWED BY (col_name, col_name, ...)                  -- (Note: Available in Hive 0.10.0 and later)]
     ON ((col_value, col_value, ...), (col_value, col_value, ...), ...)
     [STORED AS DIRECTORIES]
  [
   [ROW FORMAT row_format] 
   [STORED AS file_format]
     | STORED BY 'storage.handler.class.name' [WITH SERDEPROPERTIES (...)]  -- (Note: Available in Hive 0.6.0 and later)
  ]
  [LOCATION hdfs_path]
  [TBLPROPERTIES (property_name=property_value, ...)]   -- (Note: Available in Hive 0.6.0 and later)
  [AS select_statement];   -- (Note: Available in Hive 0.5.0 and later; not supported for external tables)
 
CREATE [TEMPORARY] [EXTERNAL] TABLE [IF NOT EXISTS] [db_name.]table_name
  LIKE existing_table_or_view_name
  [LOCATION hdfs_path];
 
data_type
  : primitive_type
  | array_type
  | map_type
  | struct_type
  | union_type  -- (Note: Available in Hive 0.7.0 and later)
 
primitive_type
  : TINYINT
  | SMALLINT
  | INT
  | BIGINT
  | BOOLEAN
  | FLOAT
  | DOUBLE
  | DOUBLE PRECISION -- (Note: Available in Hive 2.2.0 and later)
  | STRING
  | BINARY      -- (Note: Available in Hive 0.8.0 and later)
  | TIMESTAMP   -- (Note: Available in Hive 0.8.0 and later)
  | DECIMAL     -- (Note: Available in Hive 0.11.0 and later)
  | DECIMAL(precision, scale)  -- (Note: Available in Hive 0.13.0 and later)
  | DATE        -- (Note: Available in Hive 0.12.0 and later)
  | VARCHAR     -- (Note: Available in Hive 0.12.0 and later)
  | CHAR        -- (Note: Available in Hive 0.13.0 and later)
 
array_type
  : ARRAY < data_type >
 
map_type
  : MAP < primitive_type, data_type >
 
struct_type
  : STRUCT < col_name : data_type [COMMENT col_comment], ...>
 
union_type
   : UNIONTYPE < data_type, data_type, ... >  -- (Note: Available in Hive 0.7.0 and later)
 
row_format
  : DELIMITED [FIELDS TERMINATED BY char [ESCAPED BY char]] [COLLECTION ITEMS TERMINATED BY char]
        [MAP KEYS TERMINATED BY char] [LINES TERMINATED BY char]
        [NULL DEFINED AS char]   -- (Note: Available in Hive 0.13 and later)
  | SERDE serde_name [WITH SERDEPROPERTIES (property_name=property_value, property_name=property_value, ...)]
 
file_format:
  : SEQUENCEFILE
  | TEXTFILE    -- (Default, depending on hive.default.fileformat configuration)
  | RCFILE      -- (Note: Available in Hive 0.6.0 and later)
  | ORC         -- (Note: Available in Hive 0.11.0 and later)
  | PARQUET     -- (Note: Available in Hive 0.13.0 and later)
  | AVRO        -- (Note: Available in Hive 0.14.0 and later)
  | INPUTFORMAT input_format_classname OUTPUTFORMAT output_format_classname
 
constraint_specification:
  : [, PRIMARY KEY (col_name, ...) DISABLE NOVALIDATE ]
    [, CONSTRAINT constraint_name FOREIGN KEY (col_name, ...) REFERENCES table_name(col_name, ...) DISABLE NOVALIDATE 

	

     
     
 
     
Table
use ruozedata;
CREATE TABLE ruozedata_person
(id int comment 'this is id', name string comment 'this id name' )
comment 'this is ruozedata_person'
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY '\t' ;
 
create table ruozedata_emp 
(empno int, ename string, job string, mgr int, hiredate string, salary double, comm double, deptno int)
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY '\t' ;
  
 
 
CREATE table ruozedata_emp2 as select * from ruozedata_emp;
 
CREATE table ruozedata_emp3 like ruozedata_emp;
ALTER TABLE ruozedata_emp3 RENAME TO ruozedata_emp3_new;
 
create alter drop show desc 
 
创建表默认使用的是MANAGED_TABLE：内部表
    ruozedata_emp_managed
    drop：hdfs+meta
     
EXTERNAL：外部表 
create EXTERNAL table ruozedata_emp_external 
(empno int, ename string, job string, mgr int, hiredate string, salary double, comm double, deptno int)
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY '\t'
LOCATION "/ruozedata/external/emp" ;
    drop: drop meta
  
hdfs://hadoop000:8020/ddddd
s3a://xxx/yyyy 
s3n
 
create table ruozedata_emp4 like ruozedata_emp;
 
INSERT OVERWRITE TABLE ruozedata_emp4
select * FROM ruozedata_emp;
  
INSERT INTO TABLE ruozedata_emp4
SELECT empno,job, ename,mgr, hiredate, salary, comm, deptno from ruozedata_emp;
  

 #查询表结构
 
 ```
 
    > desc formatted  city_info;
OK
# col_name              data_type               comment

city_id                 int
city_name               string
area                    string

# Detailed Table Information
Database:               default
Owner:                  hadoop
CreateTime:             Fri Jun 22 22:19:30 CST 2018
LastAccessTime:         UNKNOWN
Protect Mode:           None
Retention:              0
Location:               hdfs://hadoop:9000/user/hive/warehouse/city_info
Table Type:             MANAGED_TABLE
Table Parameters:
        transient_lastDdlTime   1529677170

# Storage Information
SerDe Library:          org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe
InputFormat:            org.apache.hadoop.mapred.TextInputFormat
OutputFormat:           org.apache.hadoop.hive.ql.io.HiveIgnoreKeyTextOutputFormat
Compressed:             No
Num Buckets:            -1
Bucket Columns:         []
Sort Columns:           []
Storage Desc Params:
        field.delim             \t
        serialization.format    \t
Time taken: 0.088 seconds, Fetched: 29 row(s)
```
#   内部表改外部表 EXTER要全部大写 注意了

#DML   加载数据 
#动态分区  关闭样额模式



聚合 max
min
count




  
