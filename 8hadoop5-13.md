#到hapdoop了

##hadoop1.x 
> hdfs 存储
> MapReduce  计算+资源和作业调度

###hadoop2.x 
>>hdfs 存储
>>MapReduce  计算
>>YARN   资源和作业调度平台

#编译

MAVEN部署
2.1解压
2.2配置
3.hadoop编译
其他依赖
***** yum install -y gcc  gcc-c++ make  cmake**

yum install -y openssl openssl-devel svn ncurses-devel zlib-devel libtool
yum install -y snappy snappy-devel bzip2 bzip2-devel lzo lzo-devel lzop autoconf automake




========================================================================

hadoop安装部署
单机部署     进程没有


单机模式是Hadoop的默认模式。当首次解压Hadoop的源码包时，Hadoop无法了解硬件安装环境，便保守地选择了最小配置。
在这种默认模式下所有3个XML文件均为空。当配置文件为空时，Hadoop会完全运行在本地。
因为不需要与其他节点交互，单机模式就不使用HDFS，也不加载任何Hadoop的守护进程。
该模式主要用于开发调试MapReduce程序的应用逻辑。

作者：CoderF
链接：https://www.jianshu.com/p/99a7e0d877e6
來源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
伪分布式部署 进程存在+1节点  开发
伪分布模式在“单节点集群”上运行Hadoop，其中所有的守护进程都运行在同一台机器上。
  该模式在单机模式之上增加了代码调试功能，允许你检查内存使用情况，HDFS输入输出，以及其他的守护进程交互。
  比如namenode，datanode，secondarynamenode，jobtracer，tasktracer这5个进程，都能在集群上看到。

作者：CoderF
链接：https://www.jianshu.com/p/99a7e0d877e6
來源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
集群部署     进程存在+n节点  开发/生产
Hadoop守护进程运行在一个集群上。
  意思是说master上看到namenode,jobtracer，secondarynamenode可以安装在master节点，也可以单独安装。slave节点能看到datanode和tasktracer
下载的包: src  源代码包里面不包含jar      小
          不带src或者带bin 编译好的组件   大

4.1解压
tar -xzvf  hadoop-2.8.1.tar.gz
chown -R root:root hadoop-2.8.1
4.2解读解压文件
[root@hadoop000 hadoop-2.8.1]# ll
 
bin 执行命令的shell
etc 配置文件
lib 库
sbin 启动和关闭hadoop
share jar

#### 删除非linux的执行脚本
[root@hadoop000 hadoop-2.8.1]# rm -f bin/*.cmd
[root@hadoop000 hadoop-2.8.1]# rm -f sbin/*.cmd
[root@hadoop000 hadoop-2.8.1]# 
[root@hadoop000 hadoop-2.8.1]# ll bin   确认权限
total 348
```
-rwxrwxr-x. 1 root root 139387 Jun  2  2017 container-executor
-rwxrwxr-x. 1 root root   6514 Jun  2  2017 hadoop
-rwxrwxr-x. 1 root root  12330 Jun  2  2017 hdfs
-rwxrwxr-x. 1 root root   6237 Jun  2  2017 mapred
-rwxrwxr-x. 1 root root   1776 Jun  2  2017 rcc
-rwxrwxr-x. 1 root root 156812 Jun  2  2017 test-container-executor
-rwxrwxr-x. 1 root root  14416 Jun  2  2017 yarn
[root@hadoop000 hadoop-2.8.1]# 
```
4.3配置环境变量
[root@hadoop000 ~]# vi /etc/profile
export HADOOP_HOME=/home/ericccc/hadoop-2.8.1

export PATH=$HADOOP_HOME/bin:$PROTOC_HOME/bin:$FINDBUGS_HOME/bin:$MVN_HOME/bin:$JAVA_HOME/bin:$PATH
[root@hadoop000 ~]# source /etc/profile 执行

[root@hadoop000 ~]# which hadoop
/home/cs/hadoop-2.8.1/bin/hadoop

```
4.4配置core-site文件
<！---！>  注释用
etc/hadoop/core-site.xml:

  里面
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
</configuration>
***********单独配置******
<>etc/hadoop/hdfs-site.xml:

<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
</configuration>
```
>4.5ssh
[root@hadoop000 ~]# rm -rf .ssh

[root@hadoop000 ~]# ssh-keygen
[root@hadoop000 ~]# cd .ssh
[root@hadoop000 .ssh]# ll
total 8
-rw-------. 1 root root 1671 May 13 21:47 id_rsa
-rw-r--r--. 1 root root  396 May 13 21:47 id_rsa.pub
[root@hadoop000 .ssh]# cat id_rsa.pub >> authorized_keys
[root@hadoop000 .ssh]# 

[root@hadoop000 ~]# ssh localhost date
The authenticity of host 'localhost (::1)' can't be established.
RSA key fingerprint is ec:85:86:32:22:94:d1:a9:f2:0b:c5:12:3f:ba:e2:61.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'localhost' (RSA) to the list of known hosts.
Sun May 13 21:49:14 CST 2018
[root@hadoop000 ~]# 
[root@hadoop000 ~]# 
[root@hadoop000 ~]# ssh localhost date
Sun May 13 21:49:17 CST 2018
[root@hadoop000 ~]# 

>4.6 Format the filesystem:
#慎用  格了里面的元数据都没 ，会生成新的fsimage？？
  $ bin/hdfs namenode -format   

>4.7 java home配置
[root@hadoop000 hadoop]#      vi etc/hadoop-env.sh  ------这个目录在hadoop下的etc的hadood下 自带有！！
export JAVA_HOME=/usr/java/jdk1.8.0_45
/home/cs/jdk1.8.0_161
出现异常

/home/cs/hadoop-2.8.1/etc/hadoop/hadoop-env.sh: line 18: export: `=/home/cs/jdk1.8.0_161': not a valid identifier

`````
sbin/start-dfs.sh
[Fatal Error] mapred-site.xml:27:1: Content is not allowed in trailing section.
18/05/20 22:09:41 FATAL conf.Configuration: error parsing conf mapred-site.xml
org.xml.sax.SAXParseException; systemId: file:/home/cs/hadoop-2.8.11/etc/hadoop/mapred-site.xml; lineNumber: 27; columnNumber: 1; Content is not allowed in trailing section.
        at org.apache.xerces.parsers.DOMParser.parse(Unknown Source)

```
####   mapred-site.xml 格式里面有问题 重新检查下

>4.8 Start NameNode daemon and DataNode daemon:
[root@hadoop000 hadoop-2.8.1]# sbin/start-dfs.sh
Starting namenodes on [localhost]
localhost: starting namenode, logging to /opt/software/hadoop-2.8.1/logs/hadoop-root-namenode-hadoop000.out
localhost: starting datanode, logging to /opt/software/hadoop-2.8.1/logs/hadoop-root-datanode-hadoop000.out
Starting secondary namenodes [0.0.0.0]
The authenticity of host '0.0.0.0 (0.0.0.0)' can't be established.
RSA key fingerprint is ec:85:86:32:22:94:d1:a9:f2:0b:c5:12:3f:ba:e2:61.
Are you sure you want to continue connecting (yes/no)? yes
0.0.0.0: Warning: Permanently added '0.0.0.0' (RSA) to the list of known hosts.
0.0.0.0: starting secondarynamenode, logging to /opt/software/hadoop-2.8.1/logs/hadoop-root-secondarynamenode-hadoop000.out
[root@hadoop000 hadoop-2.8.1]# 
[root@hadoop000 hadoop-2.8.1]# 
[root@hadoop000 hadoop-2.8.1]# 
[root@hadoop000 hadoop-2.8.1]# 
[root@hadoop000 hadoop-2.8.1]# jps
16243 Jps
15943 DataNode
5127 Launcher
16139 SecondaryNameNode
15853 NameNode

[root@hadoop000 ~]# hdfs dfs -put txt.log /
[root@hadoop000 ~]# 
[root@hadoop000 ~]# 
[root@hadoop000 ~]# hdfs dfs -ls /
Found 1 items
-rw-r--r--   3 root supergroup          6 2018-05-13 21:57 /txt.log
[root@hadoop000 ~]# 
[root@hadoop000 ~]# hdfs dfs -cat /jepson.log
A
5
6
[root@hadoop000 ~]# 
[root@hadoop000 ~]# 
[root@hadoop000 ~]# cat txt.log
A
5
6
[root@hadoop000 ~]# 
