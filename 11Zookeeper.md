# HDFS写流程
HDFS CLIENT----------------------2-CREATE----------------------->nn
1.creatE dfs 返回 ------3.WRITE----- FSDARTA  outputSTREAM----------4-WRITE PACKET---DN1-----  DN2----   DN3


**记得补图**



2.pid

为什么不放到tmp  tmp里面的文件一个月会清理一次 很危险
chmod -R 777 /data/hadoop/tmp
删除pid 进程会挂吗？进程不挂 服务正常
etc/haddop/hadoop-env.sh

配置 hadoop_pid_dir=
