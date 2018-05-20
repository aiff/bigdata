# 2. bigdata
##  配置centos
### 配置网络

ipconfig -all
关闭防火墙0端口
```
打开不了5007
[hadoop@s128 sbin]$ netstat -ano |grep 50070
然后查看防火墙的状态，是否关闭，如果没有，强制性关闭

查看防火墙状态：

[hadoop@s128 sbin]$ service iptables status
关闭防火墙

 chkconfig iptables off
 service iptables stop
service iptables stop
```
> *b**iaotiyi
> root  /root
>  >xxxx   /hone/ericcc
> *  cd 切换目录
>   >cd /home/xxx

# 打印当前的目录和素有的文件夹和文件
>  ls -l ==>ll(ailaas)
>  隐藏 是以.打头的文件或者文件夹
ll -h  文件的大小
ll  -rt  按时间排序
