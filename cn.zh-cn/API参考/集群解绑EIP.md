# 集群解绑EIP<a name="ZH-CN_TOPIC_0000001387661940"></a>

## 功能介绍<a name="section13785222142718"></a>

该接口用于集群解绑EIP。

## URI<a name="section77941922152716"></a>

```
DELETE /v2/{project_id}/clusters/{cluster_id}/eips/{eip_id}
```

**表 1**  路径参数

<a name="table980782213272"></a>
<table><thead align="left"><tr id="row208021822202716"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.1"><p id="p178093226274"><a name="p178093226274"></a><a name="p178093226274"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.2"><p id="p1781222222715"><a name="p1781222222715"></a><a name="p1781222222715"></a>是否必选</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.3"><p id="p16816152218278"><a name="p16816152218278"></a><a name="p16816152218278"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="40%" id="mcps1.2.5.1.4"><p id="p17820192212275"><a name="p17820192212275"></a><a name="p17820192212275"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row180222219272"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p10824322132719"><a name="p10824322132719"></a><a name="p10824322132719"></a>project_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p782812214279"><a name="p782812214279"></a><a name="p782812214279"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p2083318223277"><a name="p2083318223277"></a><a name="p2083318223277"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p1083642272715"><a name="p1083642272715"></a><a name="p1083642272715"></a>项目ID。获取方法，请参见<a href="获取项目ID.md">获取项目ID</a>。</p>
</td>
</tr>
<tr id="row9803622102712"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p7840152222718"><a name="p7840152222718"></a><a name="p7840152222718"></a>cluster_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p9844422122712"><a name="p9844422122712"></a><a name="p9844422122712"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p08481822202713"><a name="p08481822202713"></a><a name="p08481822202713"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p785222222717"><a name="p785222222717"></a><a name="p785222222717"></a>集群ID。获取方法，请参见<a href="获取集群ID.md">获取集群ID</a>。</p>
</td>
</tr>
<tr id="row1580322216277"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p68561122202713"><a name="p68561122202713"></a><a name="p68561122202713"></a>eip_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p48601622152712"><a name="p48601622152712"></a><a name="p48601622152712"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p886415229270"><a name="p886415229270"></a><a name="p886415229270"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p68681220278"><a name="p68681220278"></a><a name="p68681220278"></a>集群绑定的弹性IP。</p>
</td>
</tr>
</tbody>
</table>

## 请求参数<a name="section5871142210274"></a>

无

## 响应参数<a name="section2879162218271"></a>

无

## 请求示例<a name="section148863229278"></a>

```
https://{Endpoint}/v2/4cf650fd46704908aa071b4df2453e1e/clusters/194408fa-9d41-435c-a140-91edcf5fe519/eips/ab60b4ac-10e3-4d83-bccd-9a6a1b0ba983
```

## 响应示例<a name="section88961522142720"></a>

无

## 状态码<a name="section990413222279"></a>

<a name="zh-cn_topic_0000001437418457_status_code"></a>
<table><thead align="left"><tr id="row691019229275"><th class="cellrowborder" valign="top" width="15%" id="mcps1.1.3.1.1"><p id="p189148220275"><a name="p189148220275"></a><a name="p189148220275"></a>状态码</p>
</th>
<th class="cellrowborder" valign="top" width="85%" id="mcps1.1.3.1.2"><p id="p10918122212273"><a name="p10918122212273"></a><a name="p10918122212273"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row1791042218279"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p17923922132713"><a name="p17923922132713"></a><a name="p17923922132713"></a>200</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p1592642212271"><a name="p1592642212271"></a><a name="p1592642212271"></a>集群解绑EIP成功。</p>
</td>
</tr>
<tr id="row1648174719241"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p0649104782416"><a name="p0649104782416"></a><a name="p0649104782416"></a>400</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p1649174782412"><a name="p1649174782412"></a><a name="p1649174782412"></a>请求错误。</p>
</td>
</tr>
<tr id="row1176335313248"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p1076318534245"><a name="p1076318534245"></a><a name="p1076318534245"></a>401</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p17764753102420"><a name="p17764753102420"></a><a name="p17764753102420"></a>鉴权失败。</p>
</td>
</tr>
<tr id="row138555910243"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p638516590245"><a name="p638516590245"></a><a name="p638516590245"></a>403</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p15385859142410"><a name="p15385859142410"></a><a name="p15385859142410"></a>没有操作权限。</p>
</td>
</tr>
<tr id="row196416110253"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p146415152519"><a name="p146415152519"></a><a name="p146415152519"></a>404</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p1564161192511"><a name="p1564161192511"></a><a name="p1564161192511"></a>找不到资源。</p>
</td>
</tr>
<tr id="row2103125692420"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p8103105622415"><a name="p8103105622415"></a><a name="p8103105622415"></a>500</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p5103175632412"><a name="p5103175632412"></a><a name="p5103175632412"></a>服务内部错误。</p>
</td>
</tr>
<tr id="row162211550172410"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p522155010241"><a name="p522155010241"></a><a name="p522155010241"></a>503</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p62212505241"><a name="p62212505241"></a><a name="p62212505241"></a>服务不可用。</p>
</td>
</tr>
</tbody>
</table>

