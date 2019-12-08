#  新课HDFS的结构



### 1  hdfs

![hdfs](https://github.com/aiff/bigdata/blob/master/img/hdfs.png)

### 2 block
大小  64m    128m（看文档咯）
参数  hdfs-site.xml    dfs.locksize
1个文件 130m  放到2个瓶子  128m  2m


### 3.副本数

dfs.replication

NameNode： 文件系统的命名空间(面试题)
         1.文件名称
	 2.文件目录结构
	 3.文件的属性(权限 创建时间 副本数)
	 4.文件对应哪些数据块-->数据块对应哪些分布在哪些DN节点上 列表  
	 
	 存储在内存上
       

DataNode: 存储数据块+ 数据块的校验和 
         与NN通信:
	 1.每隔3秒发送1次心跳 
	 2.每隔10次心跳发送一次blockReport

	 存储在磁盘上

SecondaryNameNode: 当HA时，SNN不存在了
         存储: 命令空间镜像文件fsimage + 编辑日志editlog
	 作用: 定期合并 fsimage +editlog 为新的fsimage,推送给NN，称为检查点 checkpoint
	 参数: dfs.namenode.checkpoint.period 3600s

	 实验: NN损坏，SNN去恢复
	 http://hmilyzhangl.iteye.com/blog/1407214
	 
	 
	 nn和snn的关系
	 
edits_0000000000000000308-0000000000000000324
fsimage_0000000000000000307
fsimage_0000000000000000307.md5
fsimage_0000000000000000324
fsimage_0000000000000000324.md5

fsimage_0000000000000000307 + edits_0000000000000000308-0000000000000000324
nn
NN
edits_0000000000000000306-0000000000000000307
edits_0000000000000000308-0000000000000000324
edits_inprogress_0000000000000000325


