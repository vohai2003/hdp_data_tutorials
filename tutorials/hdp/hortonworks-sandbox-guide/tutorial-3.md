---
title: Sandbox Port Forwards - HDP 3.0.1
---

# Sandbox Port Forwards - HDP 3.0.1

## Introduction

Listed below are the ports that the HDP Sandbox forwards by default, and what software or purpose each port corresponds to.

The current [architecture](https://hortonworks.com/tutorial/sandbox-architecture/) uses NGINX as a reverse proxy and only open necessary ports.

> NOTE: HDP 3.0.1 **Sandbox** is not CDA ready. CDA will remain disabled until further notice.

## Port Forwards

~~~nginx
2122  ->  22      HostSSH
2200  ->  22      HostSSH2
2222  ->  2222    DockerSSH
7777  ->  7777    Streaming Analytics Manager
8585  ->  8585    Streams Messaging Manager
7788  ->  7788    Schema Registry
8000  ->  8000    Storm Logviewer
9995  ->  9995    Zeppelin1
9996  ->  9996    Zeppelin2
9088  ->  9088    NiFi Protocol
61080 ->  61080   NiFi Registry
8886  ->  8886    AmbariInfra
61888 ->  61888   Log Search
10500 ->  10500   HS2v2
4040  ->  4040    Spark
4200  ->  4200    AmbariShell
8983  ->  8983    SolrAdmin
42080 ->  80      Apache
42111 ->  42111   nfs
8020  ->  8020    HDFS
8040  ->  8040    nodemanager
8032  ->  8032    RM
8080  ->  8080    ambari
8443  ->  8443    Knox
8744  ->  8744    StormUI
1080  ->  1080    Splash Page
8993  ->  8993    Solr
10000 ->  10000   HS2
10001 ->  10001   HS2Http
10002 ->  10002   HiveJDBCJar
30800 ->  30800   DAS
11000 ->  11000   Oozie
15000 ->  15000   Falcon
19888 ->  19888   JobHistory
50070 ->  50070   WebHdfs
50075 ->  50075   Datanode
50095 ->  50095   Accumulo
50111 ->  50111   WebHcat
16010 ->  16010   HBaseMaster
16030 ->  16030   HBaseRegion
60080 ->  60080   WebHBase
6080  ->  6080    XASecure
18080 ->  18080   SparkHistoryServer
8042  ->  8042    NodeManager
21000 ->  21000   Atlas
8889  ->  8889    Jupyter
8088  ->  8088    YARN
2181  ->  2181    Zookeeper
9090  ->  9090    Nifi
4557  ->  4557    NiFi DistributedMapCacheServer
6627  ->  6627    Storm Nimbus Thrift
9000  ->  9000    HST
6667  ->  6667    Kafka
9091  ->  9091    NiFi UI HTTPS
2202  ->  2202    Sandbox SSH 2
8188  ->  8188    YarnATS
8198  ->  8198    YarnATSR
9089  ->  9089    Druid1
8081  ->  8081    Druid2
2201  ->  2201    SSH HDP CDA

18081 ->  18081   Port for custom use
10015 ->  10015   Port for custom use
10016 ->  10016   Port for custom use
10502 ->  10502   Port for custom use
33553 ->  33553   Port for custom use
39419 ->  39419   Port for custom use
15002 ->  15002   Port for custom use
111   ->  111     Port for custom use
2049  ->  2049    Port for custom use
4242  ->  4242    Port for custom use
50079 ->  50079   Port for custom use
3000  ->  3000    Port for custom use
16000 ->  16000   Port for custom use
16020 ->  16020   Port for custom use
15500 ->  15500   Port for custom use
15501 ->  15501   Port for custom use
15502 ->  15502   Port for custom use
15503 ->  15503   Port for custom use
15504 ->  15504   Port for custom use
15505 ->  15505   Port for custom use
8765  ->  8765    Port for custom use
8090  ->  8090    Port for custom use
8091  ->  8091    Port for custom use
8005  ->  8005    Port for custom use
8086  ->  8086    Port for custom use
8082  ->  8082    Port for custom use
60000 ->  60000   Port for custom use
~~~