#��װmysql���ݿ�5.6  ������
>��װjdk 
.....
``�û��仯ʱ�� Ҫ���� chowm -R root��root xxxjdk``
****************8

#��������û�
useradd
groupadd
#creat  /etc/my.cnf
��� vi  gg��һ�е�һ��dG
��Ȩ��cnf chown chmod 
>[root@sht-sgmhadoopnn-01 local]# chown  mysqladmin:dba /etc/my.cnf 
[root@sht-sgmhadoopnn-01 local]# chmod  640 /etc/my.cnf  
[root@sht-sgmhadoopnn-01 etc]# ll my.cnf
-rw-r----- 1 mysqladmin dba 2201 Aug 25 23:09 my.cnf

[root@sht-sgmhadoopnn-01 local]# chown -R mysqladmin:dba /usr/local/mysql
[root@sht-sgmhadoopnn-01 local]# chmod -R 755 /usr/local/mysql 
[root@sht-sgmhadoopnn-01 local]# su - mysqladmin 

scripts/mysql_install_db   ��װǰ su - mydsqlxx  �л����û�
>���ÿ������� cp support-files/mysql.server /etc/rc.d/init.d/mysql
##ûд�� ����������
