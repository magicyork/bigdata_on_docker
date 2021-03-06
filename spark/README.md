## Run Spark Cluster within Docker Containers / [中文](README-CN.md)
>Before you start, make sure you have cloned this repository locally.


### 3 Nodes Spark Cluster

##### 1. pull docker image 
```
docker pull registry.cn-shenzhen.aliyuncs.com/hsdocker2019/hs_spark-hadoop:v1.0
docker tag registry.cn-shenzhen.aliyuncs.com/hsdocker2019/hs_spark-hadoop:v1.0 hs_spark-hadoop:v1.0
```

##### 2. create hadoop network

```
docker network create --driver=bridge hadoop
```

##### 3. start container

```
sh start-container.sh
```

**output:**
```
start spark master container...
start spark slave-0 container...
start spark slave-1 container...
root@master:~# 
```

>after that , you start 3 containers with 1 master and 2 slaves,you will get into the `/root` directory of master container  
>3 nodes are: master,slave-0,slave-1

##### 4. start hadoop
```
hdfs namenode -format
sh start-hadoop.sh
```

##### 5. start spark
```
sh start-spark.sh
```

test if spark's ok
```
spark-shell
```
### Arbitrary size Spark cluster
```
sh start-container.sh <number of slaves>
```

### get into master again
```
docker exec -it master bash
```

**Note: The following port mapping table is used by default**

Host port | Container port | Description
------| --- | ----
10070 | 50070 | Hadoop NameNode Web Page
18088 | 8088 | Hadoop ResourceManager Web Page
18086 | 4040 | Spark Jobs Web Page
18087 | 8080 | Spark master Web Page
1800X | 50075 | Hadoop DataNode Web Page

>X indicates the label of the slave, starting from 0    
>visit Hadoop NameNode Web: http://localhost:10070