```
1、GET /_cat/aliases?v
```
看到集群中有哪些索引别名

alias  index filter routing.index routing.search
alias1 test1 -      -            -
alias2 test1 *      -            -
alias3 test1 -      1            1
alias4 test1 -      2            1,2

```
2、GET /_cat/allocation?v
```

看到每个节点分配了几个shard，对磁盘的占用空间大小，使用率，等等

shards disk.indices disk.used disk.avail disk.total disk.percent host      ip        node
     5         260b    47.3gb     43.4gb    100.7gb           46 127.0.0.1 127.0.0.1 CSUXak2
```	 
3、GET /_cat/count?v
```
看每个索引的document数量

epoch      timestamp count
1475868259 15:24:20  120
```
4、GET /_cat/fielddata?v
```
看每个节点的jvm heap内存中的fielddata内存占用情况（对分词的field进行聚合/排序要用jvm heap中的正排索引，fielddata）

id                     host      ip        node    field   size
Nqk-6inXQq-OxUfOUI8jNQ 127.0.0.1 127.0.0.1 Nqk-6in body    544b
Nqk-6inXQq-OxUfOUI8jNQ 127.0.0.1 127.0.0.1 Nqk-6in soul    480b
```
5、GET /_cat/health?v
```
比较全面的看一个es集群的整体健康状况，主要是看是green，yellow，red

epoch      timestamp cluster       status node.total node.data shards pri relo init unassign pending_tasks max_task_wait_time active_shards_percent
1475871424 16:17:04  elasticsearch green           1         1      5   5    0    0        0             0                  -                100.0%
```
6、GET /_cat/indices?v
```
每个索引的具体的情况，比如有几个shard，多少个document，被删除的document有多少，占用了多少磁盘空间

health status index    uuid                   pri rep docs.count docs.deleted store.size pri.store.size
yellow open   twitter  u8FNjxh8Rfy_awN11oDKYQ   1   1       1200            0     88.1kb         88.1kb
```
7、GET /_cat/master?v
```
看master node当前的具体的情况，哪个node是当前的master node

id                     host      ip        node
YzWoH_2BT-6UjVGDyPdqYg 127.0.0.1 127.0.0.1 YzWoH_2
```
8、GET /_cat/nodes?v
```
看每个node的具体的情况，就比如jvm heap内存使用率，内存使用率，cpu load，是什么角色

ip        heap.percent ram.percent cpu load_1m load_5m load_15m node.role master name
127.0.0.1           65          99  42    3.07                  mdi       *      mJw06l1
```
9、GET /_cat/pending_tasks?v
```
看当前pending没执行完的task的具体情况，执行的是什么操作

insertOrder timeInQueue priority source
       1685       855ms HIGH     update-mapping [foo][t]
       1686       843ms HIGH     update-mapping [foo][t]
       1693       753ms HIGH     refresh-mapping [foo][[t]]
       1688       816ms HIGH     update-mapping [foo][t]
       1689       802ms HIGH     update-mapping [foo][t]
       1690       787ms HIGH     update-mapping [foo][t]
       1691       773ms HIGH     update-mapping [foo][t]
```	   
10、GET /_cat/plugins?v&s=component&h=name,component,version,description
```
看当前集群安装了哪些插件

name    component               version   description
U7321H6 analysis-icu            5.5.1 The ICU Analysis plugin integrates Lucene ICU module into elasticsearch, adding ICU relates analysis components.
U7321H6 analysis-kuromoji       5.5.1 The Japanese (kuromoji) Analysis plugin integrates Lucene kuromoji analysis module into elasticsearch.
U7321H6 analysis-phonetic       5.5.1 The Phonetic Analysis plugin integrates phonetic token filter analysis with elasticsearch.
U7321H6 analysis-smartcn        5.5.1 Smart Chinese Analysis plugin integrates Lucene Smart Chinese analysis module into elasticsearch.
U7321H6 analysis-stempel        5.5.1 The Stempel (Polish) Analysis plugin integrates Lucene stempel (polish) analysis module into elasticsearch.
U7321H6 analysis-ukrainian        5.5.1 The Ukrainian Analysis plugin integrates the Lucene UkrainianMorfologikAnalyzer into elasticsearch.
U7321H6 discovery-azure-classic 5.5.1 The Azure Classic Discovery plugin allows to use Azure Classic API for the unicast discovery mechanism
U7321H6 discovery-ec2           5.5.1 The EC2 discovery plugin allows to use AWS API for the unicast discovery mechanism.
U7321H6 discovery-file          5.5.1 Discovery file plugin enables unicast discovery from hosts stored in a file.
U7321H6 discovery-gce           5.5.1 The Google Compute Engine (GCE) Discovery plugin allows to use GCE API for the unicast discovery mechanism.
U7321H6 ingest-attachment       5.5.1 Ingest processor that uses Apache Tika to extract contents
U7321H6 ingest-geoip            5.5.1 Ingest processor that uses looksup geo data based on ip adresses using the Maxmind geo database
U7321H6 ingest-user-agent       5.5.1 Ingest processor that extracts information from a user agent
U7321H6 jvm-example             5.5.1 Demonstrates all the pluggable Java entry points in Elasticsearch
U7321H6 lang-javascript         5.5.1 The JavaScript language plugin allows to have javascript as the language of scripts to execute.
U7321H6 lang-python             5.5.1 The Python language plugin allows to have python as the language of scripts to execute.
U7321H6 mapper-attachments      5.5.1 The mapper attachments plugin adds the attachment type to Elasticsearch using Apache Tika.
U7321H6 mapper-murmur3          5.5.1 The Mapper Murmur3 plugin allows to compute hashes of a field's values at index-time and to store them in the index.
U7321H6 mapper-size             5.5.1 The Mapper Size plugin allows document to record their uncompressed size at index time.
U7321H6 store-smb               5.5.1 The Store SMB plugin adds support for SMB stores.
```
11、GET _cat/recovery?v
```
看shard recovery恢复的一个过程的具体情况

index   shard time type  stage source_host source_node target_host target_node repository snapshot files files_recovered files_percent files_total bytes bytes_recovered bytes_percent bytes_total translog_ops translog_ops_recovered translog_ops_percent

twitter 0     13ms store done  n/a         n/a         node0       node-0      n/a        n/a      0     0               100%          13          0     0               100%          9928        0            0                      100.0%
```
12、GET /_cat/repositories?v
```
查看用于snapshotting的repository有哪些

id    type
repo1   fs
repo2   s3
```
13、GET /_cat/thread_pool?v
```
看每个线程池的具体的情况

Z6MkIvC bulk                0 0 0
Z6MkIvC fetch_shard_started 0 0 0
Z6MkIvC fetch_shard_store   0 0 0
Z6MkIvC flush               0 0 0
Z6MkIvC force_merge         0 0 0
Z6MkIvC generic             0 0 0
Z6MkIvC get                 0 0 0
Z6MkIvC index               0 0 0
Z6MkIvC listener            0 0 0
Z6MkIvC management          1 0 0
Z6MkIvC refresh             0 0 0
Z6MkIvC search              0 0 0
Z6MkIvC snapshot            0 0 0
Z6MkIvC warmer              0 0 0
```
14、GET _cat/shards?v
```
看每个shard的具体的情况

twitter 0 p STARTED 3014 31.1mb 192.168.56.10 H5dfFeA
twitter 0 r UNASSIGNED
```
15、GET /_cat/segments?v
```
看每个segement，索引segment文件的情况，在哪个node上，有多少个document，占用了多少磁盘空间，有多少数据在内存中，是否可以搜索

index shard prirep ip        segment generation docs.count docs.deleted size size.memory committed searchable version compound
test  3     p      127.0.0.1 _0               0          1            0  3kb        2042 false     true       6.5.1   true
test1 3     p      127.0.0.1 _0               0          1            0  3kb        2042 false     true       6.5.1   true
```
16、GET /_cat/snapshots?v&s=id
```
看当前执行的snapshot的操作

id     status start_epoch start_time end_epoch  end_time duration indices successful_shards failed_shards total_shards
snap1  FAILED 1445616705  18:11:45   1445616978 18:16:18     4.6m       1                 4             1            5
snap2 SUCCESS 1445634298  23:04:58   1445634672 23:11:12     6.2m       2                10             0           10
```
17、GET /_cat/templates?v&s=name
```
看当前有那些tempalte，具体的情况是什么

name      template order version
template0 te*      0
template1 tea*     1
template2 teak*    2     7