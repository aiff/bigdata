#最小化版本的centos perl都没有的
 yum -y install perl perl-devel
 ATAL ERROR: please install the following Perl modules before executing
 yum install -y perl-Data-Dumper 
#安装mysql数据库5.6  不常用
>安装jdk 
.....
``用户变化时间 要调整 chowm -R root：root xxxjdk``
drwxr-xr-x. 8 uucp  143      4096 Apr 11  2015 jdk1.8.0_45
[root@hadoop000 java]# chown -R root:root jdk1.8.0_45
****************

#建立组和用户
useradd
groupadd
#creat  /etc/my.cnf
清空 vi  gg第一行第一字dG
授权给cnf chown chmod 
>[root@sht-sgmhadoopnn-01 local]# chown  mysqladmin:dba /etc/my.cnf 
[root@sht-sgmhadoopnn-01 local]# chmod  640 /etc/my.cnf  
给用户增加执行权限
chmod u+x a.txt

给用户所属组增加写权限，其他用户删除读权限
chmod g+w,o-r a.txt

给用户所属组增加读写执行权限
chmod g=rwx a.txt
绝对模式
绝对模式的典型范例

#模     式	意义
>777	所有用户都对文件具有读、写和执行权限
>755	文件所有者对文件具有读、写和执行权限;组用户和其他用户对文件需有读和执行权限
>711	文件所有者对文件具有读、写和执行权限;组用户和其他用户对文件具有执行权限
>644	文件所有者可以读、写文件;组用户和其他用户可以读文件
>640	文件所有者可以读、写文件;组用户可以读文件;其他用户不能访问文件
[root@sht-sgmhadoopnn-01 etc]# ll my.cnf
-rw-r----- 1 mysqladmin dba 2201 Aug 25 23:09 my.cnf

[root@sht-sgmhadoopnn-01 local]# chown -R mysqladmin:dba /usr/local/mysql
[root@sht-sgmhadoopnn-01 local]# chmod -R 755 /usr/local/mysql 
[root@sht-sgmhadoopnn-01 local]# su - mysqladmin 

scripts/mysql_install_db   安装前 su - mydsqlxx  切换到用户
### >设置开机启用 cp support-files/mysql.server /etc/rc.d/init.d/mysql
##没写完 待续！！！



### 


[root@sht-sgmhadoopnn-01 ~]# cd /usr/local/mysql
#将服务文件拷贝到init.d下，并重命名为mysql
[root@sht-sgmhadoopnn-01 mysql]# cp support-files/mysql.server /etc/rc.d/init.d/mysql 
#赋予可执行权限
[root@sht-sgmhadoopnn-01 mysql]# chmod +x /etc/rc.d/init.d/mysql
#删除服务
[root@sht-sgmhadoopnn-01 mysql]# chkconfig --del mysql
#添加服务
[root@sht-sgmhadoopnn-01 mysql]# chkconfig --add mysql
[root@sht-sgmhadoopnn-01 mysql]# chkconfig --level 345 mysql on


### 9.Start mysql and to view process and listening
```
[root@sht-sgmhadoopnn-01 mysql]# su - mysqladmin
[mysqladmin@sht-sgmhadoopnn-01 ~]$ pwd
/usr/local/mysql
[mysqladmin@sht-sgmhadoopnn-01 ~]$ rm -rf my.cnf
[mysqladmin@sht-sgmhadoopnn-01 ~]$ bin/mysqld_safe &    
不要忘记，按回车键
## bin/mysqld_safe &   --default-file=/etc/my.cnf &   也可以
[root@localhost ~]#  ps -ef|grep mysqld
514        6716   3754  0 08:52 pts/0    00:00:00 /bin/sh bin/mysqld_safe
514        7371   6716  6 08:52 pts/0    00:00:03 /usr/local/mysql/bin/mysqld --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data --plugin-dir=/usr/local/mysql/lib/plugin --log-error=/usr/local/mysql/data/hostname.err --pid-file=/usr/local/mysql/data/hostname.pid --socket=/usr/local/mysql/data/mysql.sock --port=3306
root       7403   5067  0 08:53 pts/2    00:00:00 grep mysqld
```

### 关闭数据库 你有密码就要 
```C++
> mysqladmin shutdown   -uroot -p

[mysqladmin@localhost ~]$ ps -ef|grep mysqld
514        6713   5033  0 08:50 pts/1    00:00:00 grep mysqld

```C++
