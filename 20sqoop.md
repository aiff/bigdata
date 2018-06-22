#spooq
>>
插个小插曲今天设置了path环境变量
但是还要到bin的目前下才能执行  ./SQOOOP
后来子栋同学过来指点一下我是多个窗口执行的 要生效必须在要重新sorce一次
>>
text?
hadoop fs -ls  /userhadoop/

sqoop的脚本太长了
```
运行sqoop语句报错了！！！！



18/06/11 22:21:17 INFO mapreduce.Job: The url to track the job: http://localhost:8080/
18/06/11 22:21:17 INFO mapreduce.Job: Running job: job_local1090235842_0001
18/06/11 22:21:17 INFO mapred.LocalJobRunner: OutputCommitter set in config null
18/06/11 22:21:17 INFO output.FileOutputCommitter: File Output Committer Algorithm version is 1
18/06/11 22:21:17 INFO mapred.LocalJobRunner: OutputCommitter is org.apache.hadoop.mapreduce.lib.output.FileOutputCommitter
18/06/11 22:21:18 WARN mapred.LocalJobRunner: job_local1090235842_0001
org.apache.hadoop.security.AccessControlException: Permission denied: user=root, access=WRITE, inode="/":hadoop:supergroup:drwxr-xr-x
```
找了半天原来是权限搞错了  搞错了....
最好的方法 冲新编译  记得还要sudoers配上
    hadoop  ALL=(ALL)       NOPASSWD:ALL




导入

导出

作业！！1
