
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
