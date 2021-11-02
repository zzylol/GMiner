# G-Miner

G-Miner is a general distributed system aimed at graph mining over large-scale graphs.

Graph mining is one of the most important areas in data mining. However, scalable solutions for graph mining are still lacking as existing studies focus on sequential algorithms. While many distributed graph processing systems have been proposed in recent years, most of them were designed to parallelize computations such as PageRank and Breadth-First Search that keep states on individual vertices and propagate updates along edges. Graph mining, on the other hand, may generate many subgraphs whose number can far exceed the number of vertices. This inevitably leads to much higher computational and space complexity rendering existing graph systems inefficient. We propose G-Miner, a distributed system with a new architecture designed for general graph mining. G-Miner adopts a unified programming framework for implementing a wide range of graph mining algorithms. We model subgraph processing as independent tasks, and design a novel task pipeline to streamline task processing for better CPU, network and I/O utilization.


## Feature Highlights

- **General Graph Mining Schema:** G-Miner aims to provide a unified programming framework for implementing distributed algorithms for a wide range of graph mining applications. To design this framework, we have summarized common patterns of existing graphmining algorithms.

- **Task Model:** G-Miner supports asynchronous execution of various types of operations (i.e., CPU, network, disk) and efficient load balancing by modeling a graph mining job as a set of independent tasks. A task consists of three fields: sub-graph, candidates and context.

- **Task-Pipeline:** G-Miner provides the task-pipeline, which is designed to asyn-chronously process the following three major operations in G-Miner: (1) CPU computation to process the update operation on each task, (2) network communication to pull candidates from remote machines, and (3) disk writes/reads to buffer intermediate tasks on local disk of every machine.


## Getting Started

* **Dependencies Install**

To install G-Miner's dependencies (G++, MPI, JDK, HDFS), please follow the instructions in our project [webpage](http://www.cse.cuhk.edu.hk/systems/gminer/deploy.html).

[**New**] We used [ZMQ](https://github.com/zeromq/libzmq/) lib to support asynchronously communication in v1.1.0, please also install libzmq according to this [instruction](https://github.com/zeromq/libzmq/blob/master/INSTALL).


* **Build**

Please manually MODIFY the dependency path for MPI/HDFS/ZMQ in CMakeLists.txt at the root directory.

```bash
$ export GMINER_HOME=/path/to/gminer_root  # must configure this ENV
$ cd $GMINER_HOME
$ ./auto-build.sh
```

* [**Tutorials**](docs/TUTORIALS.md)


## Academic Paper

[**Eurosys 2018**] [G-Miner: An Efficient Task-Oriented Graph Mining System](docs/G-Miner-Eurosys18.pdf). Hongzhi Chen, Miao Liu, Yunjian Zhao, Xiao Yan, Da Yan, James Cheng.

[**SIGMOD DEMO 2019**] [Large Scale Graph Mining with G-Miner](docs/GMiner\_SIGMOD19.pdf). Hongzhi Chen, Xiaoxi Wang, Chenghuan Huang, Juncheng Fang, Yifan Hou, Changji Li, James Cheng

## Acknowledgement
The subgraph-centric vertex-pulling API is attributed to our prior work [G-thinker](https://arxiv.org/abs/1709.03110).

## License

Copyright 2018 Husky Data Lab, CUHK

## Issues
```
zz_y@node0:~/GMiner$ mpiexec -n 1 /users/zz_y/GMiner/release/put sample-datasets/normal_sample.adj /GMiner/normal_sample
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/usr/local/hadoop-2.6.0/share/hadoop/httpfs/tomcat/webapps/webhdfs/WEB-INF/lib/slf4j-log4j12-1.7.5.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/usr/local/hadoop-2.6.0/share/hadoop/common/lib/slf4j-log4j12-1.7.5.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/usr/local/hadoop-2.6.0/share/hadoop/kms/tomcat/webapps/kms/WEB-INF/lib/slf4j-log4j12-1.7.5.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.slf4j.impl.Log4jLoggerFactory]
readDirect: FSDataInputStream#read error:
java.lang.UnsupportedOperationException: Byte-buffer read unsupported by input stream
	at org.apache.hadoop.fs.FSDataInputStream.read(FSDataInputStream.java:146)
hdfsOpenFile(sample-datasets/normal_sample.adj): WARN: Unexpected error 255 when testing for direct read compatibility
```
