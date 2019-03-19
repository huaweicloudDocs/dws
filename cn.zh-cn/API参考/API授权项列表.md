# API授权项列表<a name="dws_02_0056"></a>

## 集群管理<a name="section15829194192310"></a>

<a name="table189053511813"></a>
<table><thead align="left"><tr id="row11911735382"><th class="cellrowborder" valign="top" width="37.39%" id="mcps1.1.5.1.1"><p id="p179173511811"><a name="p179173511811"></a><a name="p179173511811"></a>API</p>
</th>
<th class="cellrowborder" valign="top" width="18.48%" id="mcps1.1.5.1.2"><p id="p39117351281"><a name="p39117351281"></a><a name="p39117351281"></a>API功能</p>
</th>
<th class="cellrowborder" valign="top" width="23.28%" id="mcps1.1.5.1.3"><p id="p1591535987"><a name="p1591535987"></a><a name="p1591535987"></a>授权项</p>
</th>
<th class="cellrowborder" valign="top" width="20.849999999999998%" id="mcps1.1.5.1.4"><p id="p29118351780"><a name="p29118351780"></a><a name="p29118351780"></a>授权项作用域</p>
</th>
</tr>
</thead>
<tbody><tr id="row59114351487"><td class="cellrowborder" valign="top" width="37.39%" headers="mcps1.1.5.1.1 "><p id="p691153512816"><a name="p691153512816"></a><a name="p691153512816"></a>POST /v1.0/{project_id}/clusters</p>
</td>
<td class="cellrowborder" valign="top" width="18.48%" headers="mcps1.1.5.1.2 "><p id="p0334940131712"><a name="p0334940131712"></a><a name="p0334940131712"></a>创建集群</p>
</td>
<td class="cellrowborder" valign="top" width="23.28%" headers="mcps1.1.5.1.3 "><p id="p3914356815"><a name="p3914356815"></a><a name="p3914356815"></a>dws:openAPICluster:create</p>
</td>
<td class="cellrowborder" rowspan="8" valign="top" width="20.849999999999998%" headers="mcps1.1.5.1.4 "><a name="ul256051910917"></a><a name="ul256051910917"></a><ul id="ul256051910917"><li>支持：<a name="ul116171620113612"></a><a name="ul116171620113612"></a><ul id="ul116171620113612"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="row1492103518816"><td class="cellrowborder" valign="top" headers="mcps1.1.5.1.1 "><p id="zh-cn_topic_0067607266_p63863782"><a name="zh-cn_topic_0067607266_p63863782"></a><a name="zh-cn_topic_0067607266_p63863782"></a>GET /v1.0/{project_id}/clusters</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.2 "><p id="p1034614061711"><a name="p1034614061711"></a><a name="p1034614061711"></a>查询集群列表</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.3 "><p id="p139213511818"><a name="p139213511818"></a><a name="p139213511818"></a>dws:openAPICluster:list</p>
</td>
</tr>
<tr id="row109219354814"><td class="cellrowborder" valign="top" headers="mcps1.1.5.1.1 "><p id="zh-cn_topic_0067607267_p16706408"><a name="zh-cn_topic_0067607267_p16706408"></a><a name="zh-cn_topic_0067607267_p16706408"></a>GET /v1.0/{project_id}/clusters/{cluster_id}</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.2 "><p id="p335304091718"><a name="p335304091718"></a><a name="p335304091718"></a>查询集群详情</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.3 "><p id="p292635589"><a name="p292635589"></a><a name="p292635589"></a>dws:openAPICluster:getDetail</p>
</td>
</tr>
<tr id="row49233513812"><td class="cellrowborder" valign="top" headers="mcps1.1.5.1.1 "><p id="p692035181"><a name="p692035181"></a><a name="p692035181"></a>GET /v1.0/{project_id}/node_types</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.2 "><p id="p835711401176"><a name="p835711401176"></a><a name="p835711401176"></a>查询节点类型</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.3 "><p id="p8926354814"><a name="p8926354814"></a><a name="p8926354814"></a>dws:openAPIFlavors:get</p>
</td>
</tr>
<tr id="row49211357813"><td class="cellrowborder" valign="top" headers="mcps1.1.5.1.1 "><p id="p8925351489"><a name="p8925351489"></a><a name="p8925351489"></a>DELETE /v1.0/{project_id}/clusters/{cluster_id}</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.2 "><p id="p93621940151710"><a name="p93621940151710"></a><a name="p93621940151710"></a>删除集群</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.3 "><p id="p69213355817"><a name="p69213355817"></a><a name="p69213355817"></a>dws:openAPICluster:delete</p>
</td>
</tr>
<tr id="row169964384916"><td class="cellrowborder" valign="top" headers="mcps1.1.5.1.1 "><p id="p11997153810915"><a name="p11997153810915"></a><a name="p11997153810915"></a>POST /v1.0/{project_id}/clusters/{cluster_id}/restart</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.2 "><p id="p19322125051714"><a name="p19322125051714"></a><a name="p19322125051714"></a>重启集群</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.3 "><p id="p1499718381919"><a name="p1499718381919"></a><a name="p1499718381919"></a>dws:openAPICluster:restart</p>
</td>
</tr>
<tr id="row113086818146"><td class="cellrowborder" valign="top" headers="mcps1.1.5.1.1 "><p id="p631088111419"><a name="p631088111419"></a><a name="p631088111419"></a>POST /v1.0/{project_id}/clusters/{cluster_id}/resize</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.2 "><p id="p0326175012171"><a name="p0326175012171"></a><a name="p0326175012171"></a>扩容集群</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.3 "><p id="p13310184146"><a name="p13310184146"></a><a name="p13310184146"></a>dws:openAPICluster:resize</p>
</td>
</tr>
<tr id="row76613124145"><td class="cellrowborder" valign="top" headers="mcps1.1.5.1.1 "><p id="p8565115515181"><a name="p8565115515181"></a><a name="p8565115515181"></a>POST /v1.0/{project_id}/clusters/{cluster_id}/reset-password</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.2 "><p id="p9332350141718"><a name="p9332350141718"></a><a name="p9332350141718"></a>重置集群管理员密码</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.3 "><p id="p176781218145"><a name="p176781218145"></a><a name="p176781218145"></a>dws:openAPICluster:resetPassword</p>
</td>
</tr>
</tbody>
</table>

## 快照管理<a name="section936022411233"></a>

<a name="table03835269117"></a>
<table><thead align="left"><tr id="row16384112611116"><th class="cellrowborder" valign="top" width="37.39%" id="mcps1.1.5.1.1"><p id="p13384172616114"><a name="p13384172616114"></a><a name="p13384172616114"></a>API</p>
</th>
<th class="cellrowborder" valign="top" width="18.759999999999998%" id="mcps1.1.5.1.2"><p id="p43847269119"><a name="p43847269119"></a><a name="p43847269119"></a>API功能</p>
</th>
<th class="cellrowborder" valign="top" width="23.24%" id="mcps1.1.5.1.3"><p id="p93846262119"><a name="p93846262119"></a><a name="p93846262119"></a>授权项</p>
</th>
<th class="cellrowborder" valign="top" width="20.61%" id="mcps1.1.5.1.4"><p id="p638492618118"><a name="p638492618118"></a><a name="p638492618118"></a>授权项作用域</p>
</th>
</tr>
</thead>
<tbody><tr id="row13845262114"><td class="cellrowborder" valign="top" width="37.39%" headers="mcps1.1.5.1.1 "><p id="p1338452681114"><a name="p1338452681114"></a><a name="p1338452681114"></a>POST /v1.0/{project_id}/snapshots</p>
</td>
<td class="cellrowborder" valign="top" width="18.759999999999998%" headers="mcps1.1.5.1.2 "><p id="p1162520492612"><a name="p1162520492612"></a><a name="p1162520492612"></a>创建快照</p>
</td>
<td class="cellrowborder" valign="top" width="23.24%" headers="mcps1.1.5.1.3 "><p id="p1038442619115"><a name="p1038442619115"></a><a name="p1038442619115"></a>dws:openAPISnapshot:create</p>
</td>
<td class="cellrowborder" rowspan="5" valign="top" width="20.61%" headers="mcps1.1.5.1.4 "><a name="ul118584222310"></a><a name="ul118584222310"></a><ul id="ul118584222310"><li>支持：<a name="ul18554215230"></a><a name="ul18554215230"></a><ul id="ul18554215230"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="row113858268118"><td class="cellrowborder" valign="top" headers="mcps1.1.5.1.1 "><p id="p738542631118"><a name="p738542631118"></a><a name="p738542631118"></a>GET /v1.0/{project_id}/snapshots</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.2 "><p id="p261419395124"><a name="p261419395124"></a><a name="p261419395124"></a>查询快照列表</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.3 "><p id="p838512262115"><a name="p838512262115"></a><a name="p838512262115"></a>dws:openAPISnapshot:list</p>
</td>
</tr>
<tr id="row1638562631112"><td class="cellrowborder" valign="top" headers="mcps1.1.5.1.1 "><p id="p133851726101117"><a name="p133851726101117"></a><a name="p133851726101117"></a>GET /v1.0/{project_id}/snapshots/{snapshot_id}</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.2 "><p id="p20912153551214"><a name="p20912153551214"></a><a name="p20912153551214"></a>查询快照详情</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.3 "><p id="p538582621116"><a name="p538582621116"></a><a name="p538582621116"></a>dws:openAPISnapshot:getDetail</p>
</td>
</tr>
<tr id="row1338517268118"><td class="cellrowborder" valign="top" headers="mcps1.1.5.1.1 "><p id="p53850263116"><a name="p53850263116"></a><a name="p53850263116"></a>DELETE /v1.0/{project_id}/snapshots/{snapshot_id}</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.2 "><p id="p1494103112124"><a name="p1494103112124"></a><a name="p1494103112124"></a>删除快照</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.3 "><p id="p3385426111110"><a name="p3385426111110"></a><a name="p3385426111110"></a>dws:openAPISnapshot:delete</p>
</td>
</tr>
<tr id="row4385202614112"><td class="cellrowborder" valign="top" headers="mcps1.1.5.1.1 "><p id="p1638552611110"><a name="p1638552611110"></a><a name="p1638552611110"></a>POST /v1.0/{project_id}/snapshots/{snapshot_id}/actions</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.2 "><p id="p144271353152713"><a name="p144271353152713"></a><a name="p144271353152713"></a>恢复集群</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.5.1.3 "><p id="p238511265115"><a name="p238511265115"></a><a name="p238511265115"></a>dws:openAPISnapshot:restore</p>
</td>
</tr>
</tbody>
</table>

