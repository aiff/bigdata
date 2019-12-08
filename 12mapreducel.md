
## mp的一代架构
找log  如何找 

xxxx-root-dn-xxx.out.1
hadoo组件--用户--角色（dn）--机器名称.log



ps -ef|grep  namenode
![Image text](https://github.com/aiff/bigdata/blob/master/img/local.png)


RM   application Manager 应用程序管理器
     resource  scheduler   资源memory+cpu调度器
红色框    
     container   虚拟的概念  属于NM节点上 专门用mr spark等技术的最小单元
     map  task  
     
     
