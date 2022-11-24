# 集群绑定EIP<a name="ZH-CN_TOPIC_0000001387342380"></a>

## 功能介绍<a name="section1819431616277"></a>

该接口用于集群绑定EIP。

## URI<a name="section1320117167274"></a>

```
POST /v2/{project_id}/clusters/{cluster_id}/eips/{eip_id}
```

**表 1**  路径参数

<a name="table1214171617271"></a>
<table><thead align="left"><tr id="row1920931614271"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.1"><p id="p72161716162716"><a name="p72161716162716"></a><a name="p72161716162716"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.2"><p id="p82191165270"><a name="p82191165270"></a><a name="p82191165270"></a>是否必选</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.3"><p id="p1422251620277"><a name="p1422251620277"></a><a name="p1422251620277"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="40%" id="mcps1.2.5.1.4"><p id="p7226141662715"><a name="p7226141662715"></a><a name="p7226141662715"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row221051612274"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p15230151622713"><a name="p15230151622713"></a><a name="p15230151622713"></a>project_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p323491613277"><a name="p323491613277"></a><a name="p323491613277"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p2238716122710"><a name="p2238716122710"></a><a name="p2238716122710"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p1824251610276"><a name="p1824251610276"></a><a name="p1824251610276"></a>项目ID。获取方法，请参见<a href="获取项目ID.md">获取项目ID</a>。</p>
</td>
</tr>
<tr id="row121091662715"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p1024681613278"><a name="p1024681613278"></a><a name="p1024681613278"></a>cluster_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p1124913163277"><a name="p1124913163277"></a><a name="p1124913163277"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p1125314160270"><a name="p1125314160270"></a><a name="p1125314160270"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p15257116172710"><a name="p15257116172710"></a><a name="p15257116172710"></a>集群ID。获取方法，请参见<a href="获取集群ID.md">获取集群ID</a>。</p>
</td>
</tr>
<tr id="row19210121672716"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p92601916162711"><a name="p92601916162711"></a><a name="p92601916162711"></a>eip_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p11263161619276"><a name="p11263161619276"></a><a name="p11263161619276"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p526811682711"><a name="p526811682711"></a><a name="p526811682711"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p132716167274"><a name="p132716167274"></a><a name="p132716167274"></a>未绑定的弹性IP的ID。</p>
</td>
</tr>
</tbody>
</table>

## 请求参数<a name="section1127581619276"></a>

无

## 响应参数<a name="section142826169270"></a>

无

## 请求示例<a name="section929021617279"></a>

```
https://{Endpoint}/v2/4cf650fd46704908aa071b4df2453e1e/clusters/194408fa-9d41-435c-a140-91edcf5fe519/eips/ab60b4ac-10e3-4d83-bccd-9a6a1b0ba983
```

## 响应示例<a name="section129961613272"></a>

无

## 状态码<a name="section203061161279"></a>

<a name="zh-cn_topic_0000001387338932_status_code"></a>
<table><thead align="left"><tr id="row1031116162275"><th class="cellrowborder" valign="top" width="15%" id="mcps1.1.3.1.1"><p id="p1631416164276"><a name="p1631416164276"></a><a name="p1631416164276"></a>状态码</p>
</th>
<th class="cellrowborder" valign="top" width="85%" id="mcps1.1.3.1.2"><p id="p103180165277"><a name="p103180165277"></a><a name="p103180165277"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row13311121610272"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p1932211613271"><a name="p1932211613271"></a><a name="p1932211613271"></a>200</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p193251416132716"><a name="p193251416132716"></a><a name="p193251416132716"></a>集群绑定EIP成功。</p>
</td>
</tr>
<tr id="row2067311418233"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p3674164182319"><a name="p3674164182319"></a><a name="p3674164182319"></a>400</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p19674164182314"><a name="p19674164182314"></a><a name="p19674164182314"></a>请求错误。</p>
</td>
</tr>
<tr id="row16865183312231"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p886523315237"><a name="p886523315237"></a><a name="p886523315237"></a>401</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p88651333182313"><a name="p88651333182313"></a><a name="p88651333182313"></a>鉴权失败。</p>
</td>
</tr>
<tr id="row739115393236"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p173919393239"><a name="p173919393239"></a><a name="p173919393239"></a>403</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p1539123982318"><a name="p1539123982318"></a><a name="p1539123982318"></a>没有操作权限。</p>
</td>
</tr>
<tr id="row20477134492312"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p1347724462317"><a name="p1347724462317"></a><a name="p1347724462317"></a>404</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p104771744182316"><a name="p104771744182316"></a><a name="p104771744182316"></a>找不到资源。</p>
</td>
</tr>
<tr id="row535717361233"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p53574361238"><a name="p53574361238"></a><a name="p53574361238"></a>500</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p1535715367239"><a name="p1535715367239"></a><a name="p1535715367239"></a>服务内部错误。</p>
</td>
</tr>
<tr id="row17751926102317"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p475326192310"><a name="p475326192310"></a><a name="p475326192310"></a>503</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p1375122613230"><a name="p1375122613230"></a><a name="p1375122613230"></a>服务不可用。</p>
</td>
</tr>
</tbody>
</table>

