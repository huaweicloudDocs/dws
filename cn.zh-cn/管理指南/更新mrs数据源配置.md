# 更新MRS数据源配置<a name="zh-cn_topic_0065840666"></a>

## 操作场景<a name="section31806539111657"></a>

MRS的HDFS集群的如下参数配置变更时，可能造成DWS集群无法从HDFS集群导入数据。使用HDFS数据导入前，需要执行MRS数据源配置的更新操作。

<a name="table4618184514293"></a>
<table><thead align="left"><tr id="row7619194592917"><th class="cellrowborder" valign="top" width="41%" id="mcps1.1.3.1.1"><p id="p12589614152910"><a name="p12589614152910"></a><a name="p12589614152910"></a>参数名</p>
</th>
<th class="cellrowborder" valign="top" width="59%" id="mcps1.1.3.1.2"><p id="p8398249152910"><a name="p8398249152910"></a><a name="p8398249152910"></a>参数解释</p>
</th>
</tr>
</thead>
<tbody><tr id="row161974518294"><td class="cellrowborder" valign="top" width="41%" headers="mcps1.1.3.1.1 "><p id="p43291566302"><a name="p43291566302"></a><a name="p43291566302"></a>dfs.client.read.shortcircuit</p>
</td>
<td class="cellrowborder" valign="top" width="59%" headers="mcps1.1.3.1.2 "><p id="p832912693017"><a name="p832912693017"></a><a name="p832912693017"></a>是否开启本地读。</p>
</td>
</tr>
<tr id="row1261994522912"><td class="cellrowborder" valign="top" width="41%" headers="mcps1.1.3.1.1 "><p id="p33296673017"><a name="p33296673017"></a><a name="p33296673017"></a>dfs.client.read.shortcircuit.skip.checksum</p>
</td>
<td class="cellrowborder" valign="top" width="59%" headers="mcps1.1.3.1.2 "><p id="p183303633019"><a name="p183303633019"></a><a name="p183303633019"></a>本地读时是否跳过数据校验。</p>
</td>
</tr>
<tr id="row4193515322"><td class="cellrowborder" valign="top" width="41%" headers="mcps1.1.3.1.1 "><p id="p233015643013"><a name="p233015643013"></a><a name="p233015643013"></a>dfs.client.block.write.replace-datanode-on-failure.enable</p>
</td>
<td class="cellrowborder" valign="top" width="59%" headers="mcps1.1.3.1.2 "><p id="p17330156163015"><a name="p17330156163015"></a><a name="p17330156163015"></a>向HDFS写数据块发生失败时，是否替换新的节点作为副本存储位置。</p>
</td>
</tr>
<tr id="row519165173213"><td class="cellrowborder" valign="top" width="41%" headers="mcps1.1.3.1.1 "><p id="p6330196133011"><a name="p6330196133011"></a><a name="p6330196133011"></a>dfs.encrypt.data.transfer</p>
</td>
<td class="cellrowborder" valign="top" width="59%" headers="mcps1.1.3.1.2 "><p id="p719295193211"><a name="p719295193211"></a><a name="p719295193211"></a>是否开启数据加密。</p>
<div class="note" id="note3531257017930"><a name="note3531257017930"></a><a name="note3531257017930"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p4937767417930"><a name="p4937767417930"></a><a name="p4937767417930"></a>此参数仅对启用Kerberos认证的集群有效。</p>
</div></div>
</td>
</tr>
<tr id="row1461015818328"><td class="cellrowborder" valign="top" width="41%" headers="mcps1.1.3.1.1 "><p id="p233015618306"><a name="p233015618306"></a><a name="p233015618306"></a>dfs.encrypt.data.transfer.algorithm</p>
</td>
<td class="cellrowborder" valign="top" width="59%" headers="mcps1.1.3.1.2 "><p id="p1133136153015"><a name="p1133136153015"></a><a name="p1133136153015"></a>指定密钥传输的加密解密算法。</p>
</td>
</tr>
<tr id="row3912191116327"><td class="cellrowborder" valign="top" width="41%" headers="mcps1.1.3.1.1 "><p id="p691241118326"><a name="p691241118326"></a><a name="p691241118326"></a>dfs.encrypt.data.transfer.cipher.suites</p>
</td>
<td class="cellrowborder" valign="top" width="59%" headers="mcps1.1.3.1.2 "><p id="p13912191110326"><a name="p13912191110326"></a><a name="p13912191110326"></a>指定实际存储数据传输的加密解密算法。</p>
</td>
</tr>
<tr id="row46231942133316"><td class="cellrowborder" valign="top" width="41%" headers="mcps1.1.3.1.1 "><p id="p12331067307"><a name="p12331067307"></a><a name="p12331067307"></a>dfs.replication</p>
</td>
<td class="cellrowborder" valign="top" width="59%" headers="mcps1.1.3.1.2 "><p id="p14623144210337"><a name="p14623144210337"></a><a name="p14623144210337"></a>默认数据副本个数。</p>
</td>
</tr>
<tr id="row8714346173314"><td class="cellrowborder" valign="top" width="41%" headers="mcps1.1.3.1.1 "><p id="p83311663010"><a name="p83311663010"></a><a name="p83311663010"></a>dfs.blocksiz</p>
</td>
<td class="cellrowborder" valign="top" width="59%" headers="mcps1.1.3.1.2 "><p id="p633114614307"><a name="p633114614307"></a><a name="p633114614307"></a>默认数据块大小。</p>
</td>
</tr>
<tr id="row15707450113318"><td class="cellrowborder" valign="top" width="41%" headers="mcps1.1.3.1.1 "><p id="p1833110633013"><a name="p1833110633013"></a><a name="p1833110633013"></a>hadoop.security.authentication</p>
</td>
<td class="cellrowborder" valign="top" width="59%" headers="mcps1.1.3.1.2 "><p id="p137081500335"><a name="p137081500335"></a><a name="p137081500335"></a>安全认证模式。</p>
</td>
</tr>
<tr id="row8284105503320"><td class="cellrowborder" valign="top" width="41%" headers="mcps1.1.3.1.1 "><p id="p1033110623019"><a name="p1033110623019"></a><a name="p1033110623019"></a>hadoop.rpc.protection</p>
</td>
<td class="cellrowborder" valign="top" width="59%" headers="mcps1.1.3.1.2 "><p id="p102848555333"><a name="p102848555333"></a><a name="p102848555333"></a>RPC通信保护模式。</p>
</td>
</tr>
<tr id="row19749125963313"><td class="cellrowborder" valign="top" width="41%" headers="mcps1.1.3.1.1 "><p id="p6331265302"><a name="p6331265302"></a><a name="p6331265302"></a>dfs.domain.socket.path</p>
</td>
<td class="cellrowborder" valign="top" width="59%" headers="mcps1.1.3.1.2 "><p id="p874995913313"><a name="p874995913313"></a><a name="p874995913313"></a>本地使用的Domain socket路径。</p>
</td>
</tr>
</tbody>
</table>

## 前提条件<a name="section45940751111911"></a>

-   DWS集群已创建MRS数据源连接。

## 对系统的影响<a name="section178972158583"></a>

-   更新MRS数据源连接时，DWS集群会自动重启并无法提供服务。

## 操作步骤<a name="section4276196111818"></a>

1.  在DWS管理管制台，单击“集群管理“。
2.  在集群列表，单击指定集群的名称，然后单击“MRS数据源“。
3.  在MRS数据源列表中，选中需要更新的MRS数据源，在“操作“列中，单击“更新配置“。

    更新当前连接的“MRS集群状态“和“配置状态“。在更新配置时，无法创建新的连接，且会检查安全组规则是否正常并自助修复。


