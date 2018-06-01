
###  用新的chd安装包安装hive


1.授权
[root@hadoop hadoop]# chown -R hadoop:hadoop hadoop-2.6.0-cdh5.7.0
[root@hadoop hadoop]# chown -R hadoop:hadoop apache-hive-1.1.0-cdh5.7.0-bin

2.启动

/home/hadoop/hadoop-2.6.0-cdh5.7.0/sbin
start-all.sh
3.建立目录
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
  
  
  
  如果 用which  hive  查找不到hive 有一个方法 用 cd   $HIVE_HOME 来验证即可 哈哈哈哈
拷贝驱动：cp mysqldriver $HIVE_HOME/lib
配置文件修改
	cp hive-env.sh.template hive-env.sh
		HADOOP_HOME=/home/hadoop/app/hadoop-2.6.0-cdh5.7.0
		
	hive-site.xml
