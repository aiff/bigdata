# n

1.rz 弹出对话框  CRT软件才有的
2.window--》linux
  winscp 绿色

3. scp 
将文件/文件夹 从A机器传到B机器

hadoop000: 
scp jepson.log      192.168.137.141:/tmp 
scp xxx.log    root@hadoop001:/tmp 

scp -r /ruozedata root@hadoop001:/tmp 

升级版:
scp root@hadoop001:/tmp/jepson.log  /tmp


4.ssh    
ssh hadoop001                  登录其他机器
ssh root@hadoop001             登录其他机器
ssh hadoop001  date       将命令在目标机器执行，结果返回



5.ssh-keygen 做多台机器间   互相信任  
http://blog.itpub.net/30089851/viewspace-1992210/
文件夹: ~/.ssh 

生成:
rm -rf ~/.ssh
[root@hadoop000 ~]# ssh-keygen
[root@hadoop001 ~]# ssh-keygen

选择第一台作为先完善的机器
[root@hadoop000 .ssh]# cat id_rsa.pub >> authorized_keys

其他机器将id_rsa.pub发送给第一台
[root@hadoop001 .ssh]# scp id_rsa.pub  192.168.137.251:/root/.ssh/id_rsa.pub.hadoop001
[root@hadoop002 .ssh]# scp id_rsa.pub  192.168.137.251:/root/.ssh/id_rsa.pub.hadoop001
[root@hadoop003 .ssh]# scp id_rsa.pub  192.168.137.251:/root/.ssh/id_rsa.pub.hadoop001
[root@hadoop004 .ssh]# scp id_rsa.pub  192.168.137.251:/root/.ssh/id_rsa.pub.hadoop001

将其他机器的id_rsa.pub追加到authorized_keys
[root@hadoop000 .ssh]# cat id_rsa.pub.hadoop001 >> authorized_keys
[root@hadoop000 .ssh]# cat id_rsa.pub.hadoop002 >> authorized_keys
[root@hadoop000 .ssh]# cat id_rsa.pub.hadoop003 >> authorized_keys
[root@hadoop000 .ssh]# cat id_rsa.pub.hadoop004 >> authorized_keys

然后将该authorized_keys分发
[root@hadoop000 .ssh]# scp authorized_keys 192.168.137.141:/root/.ssh/
[root@hadoop000 .ssh]# scp authorized_keys 192.168.137.142:/root/.ssh/
[root@hadoop000 .ssh]# scp authorized_keys 192.168.137.143:/root/.ssh/
[root@hadoop000 .ssh]# scp authorized_keys 192.168.137.144:/root/.ssh/


每台机器第一次要做: yes --> known_hosts
[root@hadoop000 .ssh]# ssh hadoop000 date
[root@hadoop000 .ssh]# ssh hadoop001 date
[root@hadoop000 .ssh]# ssh hadoop002 date
[root@hadoop000 .ssh]# ssh hadoop003 date
[root@hadoop000 .ssh]# ssh hadoop004 date


升级版(作业): A机器scp一个文件到B机器 无需密码 
A --> B

##  a   left join  b







####  
