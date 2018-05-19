###1111



## use hadoop 
1.dui对外提供服务  和集群
2.第一次驱动我们是配置当前xxx的无密码信任



处理再次shh登陆后要输入密码

```
[hadoop@hadoop000 ~]$ rm -rf .ssh
[hadoop@hadoop000 ~]$ ssh-keygen
[hadoop@hadoop000 ~]$ cd .ssh
[hadoop@hadoop000 .ssh]$ ll
total 8
-rw-------. 1 hadoop hadoop 1675 May 16 21:44 id_rsa
-rw-r--r--. 1 hadoop hadoop  398 May 16 21:44 id_rsa.pub
[hadoop@hadoop000 .ssh]$ cat id_rsa.pub >> authorized_keys
[hadoop@hadoop000 .ssh]$ chmod 600 authorized_keys
```

开服务报错
/home/cs/hadoop-2.8.11/etc/hadoop/hadoop-env.sh: line 18: export: `=/home/cs/jdk1.8.0_161': not a valid identifier
Starting namenodes on [138.147.166.7


这个是hadoop-env的格式写错了

