---
tags: 
  - Elasticsearch
---

# Elastic Search

## Install ES

1.  Download ES from website, and click to install.
    
2.  Make sure you have JDK version > 1.8
    
    ```bash
    java -version
    ```
    
3.  Go to the folder of ES
    
4.  ```bash
    bin/elasticsearch
    ```
    

## Install GUI

### DejaVu


#### Docker Installation

```
docker run -p 1358:1358 -d appbaseio/dejavu
open http://localhost:1358/
```

You can also run a specific version of **dejavu** by specifying a tag. For example, version `3.3.0` can be used by specifying the `docker run -p 1358:1358 appbaseio/dejavu:3.3.0` command.

##### Cross-origin resource sharing (CORS)

To make sure you enable CORS settings for your Elasticsearch instance, add the following lines in the `elasticsearch.yml` configuration file.

```
http.port: 9200
http.cors.allow-origin: 'http://localhost:1358'
http.cors.enabled: true
http.cors.allow-headers: X-Requested-With,X-Auth-Token,Content-Type,Content-Length,Authorization
http.cors.allow-credentials: true
```

If you are running your Elasticsearch with docker-compose, you can refer to the example [reference here](https://github.com/appbaseio/dejavu/blob/dev/docker-compose.yml).

If you are running your Elasticsearch with docker, you can use the following flags to pass the custom CORS

![65b9e4e618239f5e659fde467200f05f.png](../_resources/65b9e4e618239f5e659fde467200f05f.png)

​    

## Issue :NoNodeAvailableException

```
NoNodeAvailableException[None of the configured nodes are available: [{#transport#-1}{lq_UlumMQwicWXO8-2hUdQ}{127.0.0.1}{127.0.0.1:9300}]]
```

![es启动信息截图](https://img-blog.csdnimg.cn/20190910211307468.png)

![# cluster.name: my-application](https://img-blog.csdnimg.cn/20190911005352516.png)

Change the port align to the starting port on bash

```java
client.addTransportAddress(new TransportAddress(InetAddress.getByName("127.0.0.1"), 9301));
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190911005455269.png)

### Config example

```yml
#节点1的配置信息：
#集群名称，保证唯一
cluster.name: my‐elasticsearch
#节点名称，必须不一样
node.name: node‐1
#必须为本机的ip地址
network.host: 127.0.0.1
#服务端口号，在同一机器下必须不一样
http.port: 9200
#集群间通信端口号，在同一机器下必须不一样
transport.tcp.port: 9300
#设置集群自动发现机器ip集合
discovery.zen.ping.unicast.hosts: ["127.0.0.1:9300","127.0.0.1:9301","127.0.0.1:9302"]
```

* * *

## Building Elasticsearch Cluster

- Duplicate the folder, and **do delete the data folder rto prevent bug**.
- Set the ./config/elasticsearch.yml as follow:

```yml
http.cors.allow-origin: "*"
http.cors.enabled: true
# http.cors.allow-headers: X-Requested-With,X-Auth-Token,Content-Type,Content-Length,Authorization
# http.cors.allow-credentials: true

#节点1的配置信息：
#集群名称，保证唯一
cluster.name: my‐elasticsearch
#节点名称，必须不一样
node.name: node‐3
#必须为本机的ip地址
network.host: 127.0.0.1
#服务端口号，在同一机器下必须不一样
http.port: 9202
#集群间通信端口号，在同一机器下必须不一样
transport.tcp.port: 9302
#设置集群自动发现机器ip集合
# discovery.zen.ping.unicast.hosts: ["127.0.0.1:9300","127.0.0.1:9301","127.0.0.1:9302"]
discovery.seed_hosts: ["127.0.0.1:9300","127.0.0.1:9301","127.0.0.1:9302"]
cluster.initial_master_nodes: ["127.0.0.1:9300","127.0.0.1:9301","127.0.0.1:9302"]
```

Every node should do the similiar setting.

- Boot the each node as we did in one node

* * *

### Elasticsearch using docker to install (**Recommend**)

```bash
docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node"  docker.elastic.co/elasticsearch/elasticsearch:7.8.1
```

With CORS allowed
```bash
docker run -d --rm --name elasticsearch-test -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -e "http.cors.enabled=true" -e "http.cors.allow-origin=*" -e "http.cors.allow-headers=X-Requested-With,X-Auth-Token,Content-Type,Content-Length,Authorization" -e "http.cors.allow-credentials=true" docker.elastic.co/elasticsearch/elasticsearch-oss:7.8.1
```