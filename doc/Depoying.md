Deploying
==========

# 1 [Cluster Mode Overview](http://spark.apache.org/docs/latest/cluster-overview.html)

# 2 [Submitting Applications](http://spark.apache.org/docs/latest/submitting-applications.html)

# 3 [Spark Standalone Mode](http://spark.apache.org/docs/latest/spark-standalone.html)

## 3.1 安装
### 3.1.1 下载
```bash
 wget https://www-eu.apache.org/dist/spark/spark-2.4.3/spark-2.4.3-bin-hadoop2.7.tgz 
```

### 3.1.2 解压
```bash
tar -zxf spark-2.4.3-bin-hadoop2.7.tgz
```

### 3.1.3 配置环境变量
```bash
vim  ~/.bash_profile
```
添加如下配置，保存退出
```bash
export SPARK_HOME=/opt/spark-2.4.3-bin-hadoop2.7
export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin
```

### 3.1.4 配置文件`spark-defaults.conf`
```bash
cd $SPARK_HOME/conf
cp spark-defaults.conf.template spark-defaults.conf
vim spark-defaults.conf
```
修改如下配置，保存退出
```bash
spark.master                     spark://cdh6:7077
spark.eventLog.enabled           true
spark.eventLog.dir               hdfs://cdh1:8020/spark/eventLog
spark.serializer                 org.apache.spark.serializer.KryoSerializer
spark.driver.memory              5g
#spark.executor.extraJavaOptions  -XX:+PrintGCDetails -Dkey=value -Dnumbers="one two three"  

spark.history.fs.logDirectory=hdfs://cdh1:8020/spark/historyEventLog
spark.history.ui.port=18081
spark.history.fs.update.interval=10s
#	The number of application UIs to retain. If this cap is exceeded, then the oldest applications will be removed.
spark.history.retainedApplications=50
spark.history.fs.cleaner.enabled=false
spark.history.fs.cleaner.interval=1d
spark.history.fs.cleaner.maxAge=7d
spark.history.ui.acls.enable=false
```

### 3.1.5 修改配置文件`spark-env.sh`
```bash
cd $SPARK_HOME/conf
cp spark-env.sh.template spark-env.sh
vim spark-env.sh
```
添加如下配置，保存退出
```bash
export JAVA_HOME=/usr/local/zulu8
export SPARK_HOME=/opt/spark-2.4.3-bin-hadoop2.7
export SPARK_MASTER_IP=cdh6
export SPARK_EXECUTOR_MEMORY=1G
SPARK_MASTER_WEBUI_PORT=8082 # master SParkUI用的端口，如果不绑定，默认为8080，如果这个端口被占用，就会依次往后的端口绑定

```

### 3.1.6 slaves
```bash
cd $SPARK_HOME/conf
cp slaves.template slaves
vim slaves
```
添加如下配置，保存退出
```bash
cdh1
cdh2
cdh3
```

### 3.1.7 worker
将配置好的包发送到各Worker节点，并配置各Worker节点的环境变量

### 3.1.8 启动Spark
```bash
$SPARK_HOME/sbin/start-all.sh
$SPARK_HOME/sbin/start-history-server.sh

```

### 3.1.9 验证
在浏览器中查看spark的ui界面 
* master： [ http://cdh6:8082/ ](http://cdh6:8082/)
* worker:  [ http://cdh6:8083/ ](http://cdh6:8082/)
* History: [ http://cdh6:18081/ ](http://cdh6:18081/)




# 4 [Running Spark on Mesos](http://spark.apache.org/docs/latest/running-on-mesos.html)

# 5 [Running Spark on YARN](http://spark.apache.org/docs/latest/running-on-yarn.html)

# 6 [Running Spark on Kubernetes](http://spark.apache.org/docs/latest/running-on-kubernetes.html)















