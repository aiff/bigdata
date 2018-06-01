 hdfs启动错误
 Error: JAVA_HOME is not set and could not be found.
 修改/etc/hadoop/hadoop-env.sh中设JAVA_HOME
 export JAVA_HOME=$JAVA_HOME                  //错误，不能这么改
        export JAVA_HOME=/usr/java/jdk1.6.0_45        //正确，应该这么改
