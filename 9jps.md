###1111



## use hadoop 
1.dui�����ṩ���� ?�ͼ�Ⱥ
2.��һ���������������õ�ǰxxx������������



�����ٴ�shh��½��Ҫ��������

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

�����񱨴�
/home/cs/hadoop-2.8.11/etc/hadoop/hadoop-env.sh: line 18: export: `=/home/cs/jdk1.8.0_161': not a valid identifier
Starting namenodes on [138.147.166.7


�����hadoop-env�ĸ�ʽд����






YARNα�ֲ�ʽ����
[hadoop@hadoop000 hadoop]$ cp mapred-site.xml.template mapred-site.xml  �ǵñ���
[hadoop@hadoop000 hadoop]$ vi mapred-site.xml
<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
</configuration>


[hadoop@hadoop000 hadoop]$ vi yarn-site.xml:
<configuration>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
</configuration>


[hadoop@hadoop000 sbin]$ ./start-yarn.sh



yarn ����������
4308 SecondaryNameNode
5511 ResourceManager







 
 hadoop-2.8.1]$ hadoop jar ./share/hadoop/mapreduce/hadoop-mapreduce-examples-2.8.1.jar pi 5 10
  �ܳ��ڴ�  �ǵò���С��  


Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters 
                Bytes Read=590
        File Output Format Counters 
                Bytes Written=97
Job Finished in 262.832 seconds
Estimated value of Pi is 3.28000000000000000000  ��Ž�� ���ݲ�����


web��ַ  http://192.168.174.133:8088/cluster  ţ�Ʋ�ţ��  �ʻ�ˢ������
![pi����](https://github.com/aiff/bigdata/blob/master/img/pi.png)
        


