#spooq
>>
插个小插曲今天设置了path环境变量
但是还要到bin的目前下才能执行  ./SQOOOP
后来子栋同学过来指点一下我是多个窗口执行的 要生效必须在要重新sorce一次
>>
text?
hadoop fs -ls  /userhadoop/

sqoop的脚本太长了
```
运行sqoop语句报错了！！！！



18/06/11 22:21:17 INFO mapreduce.Job: The url to track the job: http://localhost:8080/
18/06/11 22:21:17 INFO mapreduce.Job: Running job: job_local1090235842_0001
18/06/11 22:21:17 INFO mapred.LocalJobRunner: OutputCommitter set in config null
18/06/11 22:21:17 INFO output.FileOutputCommitter: File Output Committer Algorithm version is 1
18/06/11 22:21:17 INFO mapred.LocalJobRunner: OutputCommitter is org.apache.hadoop.mapreduce.lib.output.FileOutputCommitter
18/06/11 22:21:18 WARN mapred.LocalJobRunner: job_local1090235842_0001
org.apache.hadoop.security.AccessControlException: Permission denied: user=root, access=WRITE, inode="/":hadoop:supergroup:drwxr-xr-x
```
找了半天原来是权限搞错了  搞错了....
最好的方法 冲新编译  记得还要sudoers配上
    hadoop  ALL=(ALL)       NOPASSWD:ALL




导入

导出

作业！！1



1.建立城市表
CREATE DATABASE ruozedata;

DROP TABLE city_info;
CREATE TABLE `city_info` (
  `city_id` int(11) DEFAULT NULL,
  `city_name` varchar(255) DEFAULT NULL,
  `area` varchar(255) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;


insert  into `city_info`(`city_id`,`city_name`,`area`) values (1,'BEIJING','NC'),(2,'SHANGHAI','EC'),(3,'NANJING','EC'),(4,'GUANGZHOU','SC'),(5,'SANYA','SC'),(6,'WUHAN','CC'),(7,'CHANGSHA','CC'),(8,'XIAN','NW'),(9,'CHENGDU','SW'),(10,'HAERBIN','NE');



sqoop import \
--connect jdbc:mysql://localhost:3306/ruozedata_basic03 \
--username root --password root \
--table city_info -m 1 \
--mapreduce-job-name city_info_imp \
--delete-target-dir \
--hive-table ruozedata.city_info \
--hive-import \
--fields-terminated-by '\t' \
--hive-overwrite;




2.建立生产品表






CREATE TABLE `product_info` (
  `product_id` int(11) DEFAULT NULL,
  `product_name` varchar(255) DEFAULT NULL,
  `extend_info` varchar(255) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;


3.hive  用户行为

create table user_click(user_id int,session_id string,action_time string,city_id int,product_id int)
partitioned by (create_day string)
row format delimited fields terminated by ',';
load data local inpath '/home/hadoop/data/user_click.txt' into table user_click partition(create_day='2016-05-05');


