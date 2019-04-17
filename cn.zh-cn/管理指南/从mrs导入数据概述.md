# 从MRS导入数据概述<a name="zh-cn_topic_0065840553"></a>

## 从MRS导入数据到集群<a name="section34418118183527"></a>

MapReduce服务（MapReduce Service，简称MRS）是一个基于开源Hadoop生态环境而运行的大数据集群，对外提供大容量数据的存储和分析能力，可解决用户的数据存储和处理需求。具体信息可参考《MapReduce服务用户指南》。

用户可以将海量业务数据，存储在MRS的分析集群，即使用Hive/Spark组件保存。Hive/Spark的数据文件则保存在HDFS中。DWS支持在相同网络中，配置一个DWS集群连接到一个MRS集群，然后将数据从HDFS中的文件读取到DWS。

## 导入流程<a name="section4774472184623"></a>

从MRS导入数据到集群流程如下：

1.  在DWS集群创建一个MRS数据源连接，具体操作步骤请参见[创建MRS数据源连接](创建mrs数据源连接.md)。

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >连接在数据库中使用“外部服务器“表示。一个DWS集群与一个MRS集群间只可以有一个连接，但可以从一个DWS集群连接到多个不同MRS集群。  

2.  创建一个HDFS外表，外表通过外部服务器的接口，从MRS集群查询数据。

    具体操作步骤请参见《数据仓库服务数据库开发指南》中[从MRS导入数据到集群](https://support.huaweicloud.com/devg-dws/migrate_data_from_mrs_0001.html)章节。


