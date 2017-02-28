---
title: Windows上搭建Kafka运行环境
category: Kafka
---

### 完整解决方案请参考： 

[Setting Up and Running Apache Kafka on Windows OS](https://dzone.com/articles/running-apache-kafka-on-windows-os)

 
__在环境搭建过程中遇到两个问题，在这里先列出来，以方便查询：__

1. \Java\jre7\lib\ext\QTJava.zip was unexpected at this time. Process exited

	__解决方案：__
	1.1 右键点击“我的电脑” -> "高级系统设置" -> "环境变量" 
	1.2 查看CLASSPATH的值里有没有包含QTJava.zip的路径，如果有的话，把对应的路径删除，问题就解决了。
 
2. Missing `server' JVM (Java\jre7\bin\server\jvm­­.dll.)

	__解决方案：__
	2.1 拷贝C:\Program Files\Java\jdk1.6.0\jre\bin\server
	2.2 粘贴到 C:\Program Files\Java\jre1.6.0\bin
 
# 搭建环境

## 1. 安装JDK

1.1 安装文件：http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html下载Server JRE.

1.2 安装完成后需要添加以下的环境变量（右键点击“我的电脑” -> "高级系统设置" -> "环境变量"）：

	JAVA_HOME: C:\Program Files (x86)\Java\jre1.8.0_60
	(这个是默认安装路径，如果安装过程中更改了安装目录，把更改后的路径填上就行了）
	PATH: 在现有的值后面添加"; %JAVA_HOME%\bin"

1.3 打开cmd运行 "java -version" 查看当前系统Java的版本：

	java-version

![Result](/images/Kafka/java_version.jpg)
 
## 2. 安装Zookeeper

Kafka的运行依赖于Zookeeper，所以在运行Kafka之前我们需要安装并运行Zookeeper

2.1	下载安装文件： http://zookeeper.apache.org/releases.html 

2.2	解压文件（本文解压到 G:\zookeeper-3.4.8）

2.3	打开G:\zookeeper-3.4.8\conf，把__zoo_sample.cfg__重命名成__zoo.cfg__

2.4	从文本编辑器里打开zoo.cfg

2.5	把dataDir的值改成**“:\zookeeper-3.4.8\data”**

2.6	添加如下系统变量：

	ZOOKEEPER_HOME: G:\zookeeper-3.4.8
	Path: 在现有的值后面添加 ";%ZOOKEEPER_HOME%\bin;"

2.7	运行Zookeeper: 打开cmd然后执行

	zkserver 

## 3. 安装并运行Kafka

3.1 下载安装文件： http://kafka.apache.org/downloads.html

3.2 解压文件（本文解压到 G:\kafka_2.11-0.10.0.1）

3.3 打开G:\kafka_2.11-0.10.0.1\config

3.4 从文本编辑器里打开 **server.properties**

3.5 把 log.dirs的值改成 **“G:\kafka_2.11-0.10.0.1\kafka-logs”**

3.6 打开cmd

3.7 进入kafka文件目录: 

	cd /d G:\kafka_2.11-0.10.0.1\

3.8 输入并执行以打开kafka:
	.\bin\windows\kafka-server-start.bat .\config\server.properties
 

## 4. 创建topics

4.1 打开cmd 并进入G:\kafka_2.11-0.10.0.1\bin\windows

4.2 创建一个topic:

	kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test

## 5. 打开一个Producer

	cd /d G:\kafka_2.11-0.10.0.1\bin\windows
	kafka-console-producer.bat --broker-list localhost:9092 --topic test
 

## 6. 打开一个Consumer

	cd /d G:\kafka_2.11-0.10.0.1\bin\windows
	kafka-console-consumer.bat --zookeeper localhost:2181 --topic test

然后就可以在Producer控制台窗口输入消息了。在消息输入过后，很快Consumer窗口就会显示出Producer发送的消息：
![Result](/images/Kafka/setup_result.jpg)

至此，Kafka运行环境的搭建就完成了:-)
 