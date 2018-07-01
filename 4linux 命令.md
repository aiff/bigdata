# bigdata
*出现小r参数的命令
* 出现R参数的命令
* mv cp谁快
* 查看命令帮助 你们觉得该怎么看
**领导叫你打开那台电脑xxx服务的web界面，该怎么办      
***拓展题 : 我们发现一个用户 ，登录不了，或者su也切换不了，说该用户不可登录，我们要修改什么文件，将什么修改什么
        *多人会话命令是什么? 创建，进入，退出，查看分别什么参数
        *每五分钟定时跑一个脚本，请问什么命令编辑进去，什么命令行
        *级联创建文件夹，命令和参数
        *环境变量文件分为哪两种，分别在哪，分别怎样生效
**************
 ======
```隐藏文件什么标识开始，什么命令参数查看
场景题:  一台电脑有个组件只知道名字xxx中间三个字母，请问做怎样找到它
which这个命令，是去找命令，请问是从哪个里面找的
```
+tar解压，一般会出现什么问题?
+查看文件大小哪两个命令
16.查看文件夹大小，哪个命令?
防止root 登陆 修改  vi /ext/passwd里面的文件 增加nologin
##正文
 
##  ll
>drwxr-xr-x. 2 root   root       4096 4月  12 17:12 模板
drwxr-xr-x. 2 root   root       4096 4月  12 17:12 视频
</code>code
#   第一列   
>  R 4  W 2  X  1
第一个   d文件夹   -文件  l 链接
三组  第一组 rwx 7 代表root用户对这个文件或文件夹的权限
      第二组   r-w  5  代表root用户组对这个文件或文件夹的权限
      第三组 r-x    5 代表其他组的所有用户对这个文件或文件夹的权限
##  第三列  所属的用户
###    第三列  所属的组
chmod  改文件权限  三个的总和   4+2+1 777 全部给完
chmod  646  qq.log  rw=6
./www.sh
给文件权限
### chmod   764 xx.sh
可执行  ：针对  shell脚本
chmod +x 每组都加x 注意没必要
vi shift+$  尾行
set nu 行号
set nonu
：100  定位行

## yum  ************************


</code></pre>
<code>+tar解压，一般会出现什么问题?
                            +查看文件大小哪两个命令
                            16.查看文件夹大小，哪个命令?
              防止root 登陆 修改  vi /ext/passwd里面的文件 增加nologin


##主动防御
使用 `  fail2ban `  锁定ip

*tar
 *   cd
     ***  python  setup.py install***
-16.查看文件夹大小，哪个命令?
-防止root 登陆 修改  vi /ext/passwd里面的文件 增加nologin
        
  ### rehl6.8 换     源
 ### 0查看现有的源 rpm -aq | grep yum
  1、删除rhel自带的yum源

# rpm -aq | grep yum|xargs rpm -e --nodeps

2、下载新的yum安装包
###具体地址自己更新 目前只有6.9
wget http://mirrors.163.com/CentOS/6/os/x86_64/Packages/yum-metadata-parser-1.1.2-16.el6.x86_64.rpm
wget http://mirrors.163.com/centos/6/os/x86_64/Packages/yum-3.2.29-69.el6.centos.noarch.rpm
wget http://mirrors.163.com/centos/6/os/x86_64/Packages/yum-plugin-fastestmirror-1.1.30-30.el6.noarch.rpm

3、安装yum包，注意的是标红的必须一起装，有依赖关系

rpm -ivh yum-metadata-parser-xxxx.rpm yum-3.2.29-6xxx.rpm yum-plugin-fastestmirrxxxarch.rpm

4、更改成ali的yum源

# cd /etc/yum.repos.d/

#   wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo 

# ls
CentOS6-Base-163.repo

把文件里面的$releasever全部替换为版本号，即6

# sed -i 's#$releasever#6#g' CentOS6-Base-163.repo

5、清除yum缓存

# yum clean all

# yum makecache    #将服务器上的软件包信息缓存到本地,以提高搜索安装软件的速度  gogogog!!!

