

###  HIVE QL/HQL:类sql 
SQL ===> MapReduce/Spark/Tez JOB   所有运行很慢  运行进程慢慢慢慢
###  统一的元数据管理 Mysql/Derby
hive vs    rdbms
hivelim里面的事务是鸡肋  insert自动提交

hive适用于什么场景    离线 (外部表)     
###  用新的chd安装包安装hive


> 1.授权
```
[root@hadoop hadoop]# chown -R hadoop:hadoop hadoop-2.6.0-cdh5.7.0
[root@hadoop hadoop]# chown -R hadoop:hadoop apache-hive-1.1.0-cdh5.7.0-bin
```
检查HOME路径
```
[root@hadoop001 ~]# echo $HIVE_HOME
/home/hadoop/apache-hive-1.1.0-cdh5.7.0-bin
```

> 2.启动

/home/hadoop/hadoop-2.6.0-cdh5.7.0/sbin
start-all.sh
> 3.建立目录
software  存放安装软件
	data 存放测试数据
	source 存放源代码  
	lib  存放相关开发的jar
	app  软件安装目录
		tmp 存放HDFS/Kafka/ZK数据目录
	maven_repo  maven本地仓库
	shell  存放上课相关的脚本
  
#### mkdir  software   data  source  lib   app   tmp  maven_repo   shell   
配置环境变量: ~/.bash_profile
	export HIVE_HOME=/home/hadoop/app/hive-1.1.0-cdh5.7.0
	export PATH=$HIVE_HOME/bin:$PATH
  
  
  
>  如果 用which  hive  查找不到hive 有一个方法 用 cd   $HIVE_HOME 来验证即可 哈哈哈哈
```
拷贝驱动：cp mysqldriver $HIVE_HOME/lib  找群友要一个驱动的mysql-connector-java。jar包
```
配置文件修改 cd  conf
	cp hive-env.sh.template hive-env.sh
	HADOOP_HOME=/home/hadoop/app/hadoop-2.6.0-cdh5.7.0 
	自己建立一个hive-site.xml
	
	
` 执行hive 报错` 
hive-site.xml:2:6: The processing instruction target matching "[xX][mM][lL]" is not allowed.
[Fatal Error] hive-site.xml:21:1: XML document structures must start and end within the same entity.
18/06/01 11:43:37 FATAL conf.Configuration: error parsing conf file:/home/hadoop/app/hive-1.1.0-cdh5.7.0/conf/hive-site.xml
org.xml.sax.SAXParseException; systemId: file:/home/hadoop/app/hive-1.1.0-cdh5.7.0/conf/hive-site.xml; lineNumber: 21; columnNumber: 1; XML document structures must start and end within the same entity.
![hive报错](https://github.com/aiff/bigdata/blob/master/img/hiveerror.png)
> 发现mysql和hadoop咩起来 被拒绝了  启用她们

` HIVE  建表报错` 


hive> create table xxxx(id int);
FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.DDLTask. MetaException(message:file:/user/hive/warehouse/xxxx is not a directory or unable to create one)


处理：建立路径即可

/user/hive/warehouse


 
> ` Hive启动时，报错无法找到class` 
，如java.lang.NoClassDefFoundError

Exception in thread "main" java.lang.NoClassDefFoundError: org/apache/hadoop/hi


去检查hive-env.sh  和hadoop-env.sh 

> 报错  MoveTask   查看日志
```
ERROR [main]: metastore.RetryingHMSHandler (RetryingHMSHandler.java:invokeInternal(203)) - Retrying HMSHandler after 2000 ms (attempt 6 of 10) with error: javax.jdo.JDODataStoreException: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'OPTION SQL_SELECT_LIMIT=DEFAULT' at line 1
```

处理  更换mysql驱动
 http://mvnrepository.com/artifact/mysql/mysql-connector-java/5.1.26  直接下载把  如果要学习就用maven
 <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.26</version>
</dependency>



