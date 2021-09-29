# 从MRS导入数据概述<a name="ZH-CN_TOPIC_0000001098976674"></a>

## 从MRS导入数据到集群<a name="section34418118183527"></a>

MapReduce服务（MapReduce Service，简称MRS）是一个基于开源Hadoop生态环境而运行的大数据集群，对外提供大容量数据的存储和分析能力，可解决用户的数据存储和处理需求。有关MRS服务的详细信息，请参考[《MapReduce服务用户指南》](https://support.huaweicloud.com/usermanual-mrs/mrs_01_0025.html)。

用户可以将海量业务数据，存储在MRS的分析集群，即使用Hive/Spark组件保存。Hive/Spark的数据文件则保存在HDFS中。GaussDB\(DWS\) 支持在相同网络中，配置一个GaussDB\(DWS\) 集群连接到MRS集群，然后将数据从HDFS中的文件读取到GaussDB\(DWS\) 。

## 导入流程<a name="section4774472184623"></a>

从MRS导入数据到集群流程如下：

1.  在GaussDB\(DWS\) 集群创建一个MRS数据源连接，具体操作步骤请参见[创建MRS数据源连接](创建MRS数据源连接.md)。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   同一个网络下可以有多个MRS数据源， 但是GaussDB\(DWS\)集群每次只能和一个MRS集群建立连接。

2.  创建一个HDFS外表，外表通过外部服务器的接口，从MRS集群查询数据。

    具体操作步骤请参见《数据仓库服务数据库开发指南》中[从MRS导入数据到集群](https://support.huaweicloud.com/devg-dws/dws_04_0210.html)章节。

3.  （可选）当MRS集群的HDFS配置发生变更时，在GaussDB\(DWS\) 服务中，需要执行MRS数据源配置的更新操作，详情请参见[更新MRS数据源配置](更新MRS数据源配置.md)。

