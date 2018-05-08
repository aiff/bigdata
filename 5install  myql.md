#安装mysql数据库5.6  不常用
>安装jdk 
.....
``用户变化时间 要调整 chowm -R root：root xxxjdk``
****************8

#建立组和用户
useradd
groupadd
#creat  /etc/my.cnf
清空 vi  gg第一行第一字dG
授权给cnf chown chmod 
>[root@sht-sgmhadoopnn-01 local]# chown  mysqladmin:dba /etc/my.cnf 
[root@sht-sgmhadoopnn-01 local]# chmod  640 /etc/my.cnf  
[root@sht-sgmhadoopnn-01 etc]# ll my.cnf
-rw-r----- 1 mysqladmin dba 2201 Aug 25 23:09 my.cnf

[root@sht-sgmhadoopnn-01 local]# chown -R mysqladmin:dba /usr/local/mysql
[root@sht-sgmhadoopnn-01 local]# chmod -R 755 /usr/local/mysql 
[root@sht-sgmhadoopnn-01 local]# su - mysqladmin 

scripts/mysql_install_db   安装前 su - mydsqlxx  切换到用户
>设置开机启用 cp support-files/mysql.server /etc/rc.d/init.d/mysql
##没写完 待续！！！
