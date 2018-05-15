# bigdata
# scp   文件从a机器到b机器 
> scp  xxxx.log root@hadop001:/tmp
>  scp  -r abc root@hadop001:/tmp </br>  scp  -r abc ip:/tmp
#  文件从b机器到a机器 (本机)
  scp   root@hadop001:/tmp、xxxx.log  /tmp
## ssh 
**************************
#mkdir  -p 1/2/3  创建3层目录

mkdir  4 5  6 同层
[root@localhost home]# mkdir 4 5 6
[root@localhost home]# ls
4  5  6  cs  lost+found
[root@localhost home]# ll
总用量 32
</br>drwxr-xr-x.  2 root root  4096 5月   8 18:50 4
</br>drwxr-xr-x.  2 root root  4096 5月   8 18:50 5
</br>drwxr-xr-x.  2 root root  4096 5月   8 18:50 6
</br>drwx------. 30 cs   cs    4096 4月  16 17:40 cs
</br>drwx------.  2 root root 16384 4月  11 21:43 lost+found



### bigdata</br>mv  20180427.log /home  移动文件或文件夹


### bigdata</br>  cp -r 20180427.log /home  移动文件夹用 -r小写
####  mv比cp快
-查看文件
-查看文件夹
 +   查看文件内容  cat  xx.log </br> more xx.log  一页页按空格键翻页
  </br>  实时查看内容 tail -f xx.log </br> 实时查看内容
 +  echo "334">>追加   echo "334">覆盖的 
 
####  别名     alias 设置永久 /etc/profile  
source /etc/profile  生效


个人:  .bash_profile 、.bashrc
~/.bash_profile
source ~/.bash_profile  生效
. ~/.bash_profile     生效

> 删除文件   rm  -rf  -r文件 f强制

>history !70 查看历史命令和执行第70行


#
> tail  -f   根据文件描述符进行追踪，当文件改名或被删除，追踪停止   tail  -100f  倒着查看最新100行 
>> tail  -F  --retry(被截断还调用-f)，根据文件名进行追踪，并保持重试，即该文件被删除或改名后，如果再次创建相同的文件名，会继续追踪
#
> su xxx  切换了root身份，但Shell环境仍然是普通用户的Shell；  
>>su -  xxx   连用户和Shell环境一起切换成root身份了。只有切换了Shell环境才不会出现PATH环境变量错误。su切换成root用户以后，pwd
一下，发现工作目录仍然是普通用户的工作目录；而用su -命令切换以后，工作目录变成root的工作目录了

#
> /ext/profile

Linux 系统中有软链接和硬链接两种特殊的“文件”。

软链接可以看作是Windows中的快捷方式，可以让你快速链接到目标档案或目录。

硬链接则透过文件系统的inode来产生新档名，而不是产生新档案。

创建方法都很简单：

软链接（符号链接） ln -s   source  target 
硬链接 （实体链接）ln       source  target

