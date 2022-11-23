# Top耗时SQL查看<a name="ZH-CN_TOPIC_0000001405317102"></a>

## 问题现象<a name="zh-cn_topic_0000001076579583_section821173714379"></a>

Top 5耗时的查询，存在耗时较长的SQL。

## 定位思路<a name="zh-cn_topic_0000001076579583_section386655614379"></a>

通过集群概览页面的Top5耗时的查询子页面，记录Top5耗时查询的变化历史记录。

通过分析Top5查询出现的频率，定位慢查询。

## 解决步骤<a name="zh-cn_topic_0000001076579583_section69919963819"></a>

1.  查看“集群概览”页面的“Top5耗时查询”页面。
2.  <a name="zh-cn_topic_0000001076579583_li4816105212416"></a>找到耗时较长的SQL查询ID，通过数据库视图PGXC\_WLM\_SESSION\_STATISTICS查询到pid字段\(session\_id\)。
3.  在“会话监控”页面，找到[2](#zh-cn_topic_0000001076579583_li4816105212416)查出的session\_id（即会话ID），将执行时间过长的SQL杀掉。

