# 1 安装Java

[JVM安装(linux)](../JVM/JVM安装(linux).md)

# 2 安装hadoop

1. 配置免密登录

```
ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 0600 ~/.ssh/authorized_keys
```

> ssh localhost 不提示输入密码，就说明配置成功

2. 添加环境变量

```
export HADOOP_HOME=/root/cluster/hadoop-2.8.3
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
```

3. 修改配置

core-site.xml

```xml
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://192.168.56.3:9000</value>
    </property>
    <property>
        <name>hadoop.tmp.dir</name>
        <value>/root/cluster/hadoop-2.8.3/tmp</value>
    </property>
</configuration>
```

hdfs-site.xml

```xml
<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
</configuration>
```

yarn-site.xml

```xml
<configuration>
  <property>
    <name>yarn.nodemanager.aux-service</name>
    <value>mapreduce_shuffle</value>
  </property>
</configuration>
```

mapred-site.xml

```xml
<configuration>
  <property>
    <name>mapreduce.framewok.name</name>
    <value>yarn</value>
  </property>
</configuration>
```

4. 启动HDFS和YARN

```
hadoop namenode -format
start-all.sh
```
