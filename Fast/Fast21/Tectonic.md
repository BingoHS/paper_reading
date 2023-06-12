# Tectonic : Facebook新一代分布式文件系统

## Background推荐补充

《Finding a Needle in Haystack: Facebook’s Photo Storage.》 

《HDFS Architecture Guide》

《f4: Facebook’s Warm BLOB Storage System.》

分别讲述了Haystack, HDFS, f4三种facebook之前的存储结构

《Azure
Data Lake Store: a hyperscale distributed file service
for big data analytics.》主要讲了Facebook之前处理元数据的扩展问题
## 引出问题

在之前的存储方案中，Facebook不同种类的存储数据存储在不同种存储结构之中，这使得运营和资源十分麻烦，所以就引出了文章的主题：统一各种资源的存储。

Tectonic系统面临三个挑战：扩展存储系统的规模(eb级别)；提供租户之间的性能隔离；以及对于特定租户的优化

Haystack：高访问频率&复制实现高可用（空间效率低）

f4：吞吐量次于haystack，但空间效率高

结论：两种存储系统互相拥有对方急缺的资源

这里涉及到一个逻辑推导，在硬盘发展的过程中，容量不断扩增，但IOPS维持不变，这样就会导致单位容量的IOPS能力下降，就会使得Haystack这样需要高IOPS能力的存储系统受限。之前会使用额外的高吞吐量做额外读写盘，但空间放大会更严重。

HDFS用来做数据仓库的问题：主要是由于HDFS元数据存储在单个节点上，这个瓶颈导致单个存储系统存储性能是有上界的，但现在这个limit明显限制了数据扩张的数据仓库应用，简单来说就是存储空间不够了

## Tectonic结构

![Tectonic顶层架构](Tectonic_top_arc.png "")
这张图相对理解的内容比较少，可以理解为Tectonic有多个数据中心，可以做到host、rack等小级别的高可用容错。数据中心的高可用容错是用户来操控。

![Tectonic单个集群架构](tectonic_cluster_arc.png)

集群由存储节点、元数据节点和用于后台操作的无状态节点组成。






