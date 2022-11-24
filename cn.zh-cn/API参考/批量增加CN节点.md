# 批量增加CN节点<a name="ZH-CN_TOPIC_0000001437702057"></a>

## 功能介绍<a name="section8426163919179"></a>

该接口用于为指定集群批量增加CN节点。

## URI<a name="section84361839141714"></a>

```
POST /v1.0/{project_id}/clusters/{cluster_id}/cns/batch-create
```

**表 1**  路径参数

<a name="table545283971713"></a>
<table><thead align="left"><tr id="row1344613951717"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.1"><p id="p64559396170"><a name="p64559396170"></a><a name="p64559396170"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.2"><p id="p124601939191711"><a name="p124601939191711"></a><a name="p124601939191711"></a>是否必选</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.3"><p id="p54668397174"><a name="p54668397174"></a><a name="p54668397174"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="40%" id="mcps1.2.5.1.4"><p id="p247053920178"><a name="p247053920178"></a><a name="p247053920178"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row1644773910174"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p147503961718"><a name="p147503961718"></a><a name="p147503961718"></a>project_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p148153910171"><a name="p148153910171"></a><a name="p148153910171"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p1348713911173"><a name="p1348713911173"></a><a name="p1348713911173"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p4492539191720"><a name="p4492539191720"></a><a name="p4492539191720"></a>项目ID。获取方法，请参见<a href="获取项目ID.md">获取项目ID</a>。</p>
</td>
</tr>
<tr id="row744753914176"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p049713396170"><a name="p049713396170"></a><a name="p049713396170"></a>cluster_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p10501123916176"><a name="p10501123916176"></a><a name="p10501123916176"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p1506153921712"><a name="p1506153921712"></a><a name="p1506153921712"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p4511133919175"><a name="p4511133919175"></a><a name="p4511133919175"></a>集群的ID。获取方法，请参见<a href="获取集群ID.md">获取集群ID</a>。</p>
</td>
</tr>
</tbody>
</table>

## 请求参数<a name="section195165394174"></a>

**表 2**  请求Body参数

<a name="zh-cn_topic_0000001437538225_request_V1BatchCreateCnRequestBody"></a>
<table><thead align="left"><tr id="row165228393179"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.1"><p id="p1253083920177"><a name="p1253083920177"></a><a name="p1253083920177"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.2"><p id="p105351539141714"><a name="p105351539141714"></a><a name="p105351539141714"></a>是否必选</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.3"><p id="p1353914392174"><a name="p1353914392174"></a><a name="p1353914392174"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="40%" id="mcps1.2.5.1.4"><p id="p3545739121714"><a name="p3545739121714"></a><a name="p3545739121714"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row1522143912173"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p9549143917177"><a name="p9549143917177"></a><a name="p9549143917177"></a>num</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p15542396170"><a name="p15542396170"></a><a name="p15542396170"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p5558143971719"><a name="p5558143971719"></a><a name="p5558143971719"></a>Integer</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p256433971711"><a name="p256433971711"></a><a name="p256433971711"></a>批量增加CN节点数量。</p>
</td>
</tr>
</tbody>
</table>

## 响应参数<a name="section11570143911720"></a>

**状态码： 200**

**表 3**  响应Body参数

<a name="zh-cn_topic_0000001437538225_response_V1BatchCreateCnResponseBody"></a>
<table><thead align="left"><tr id="row175803396177"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.4.1.1"><p id="p55871039181710"><a name="p55871039181710"></a><a name="p55871039181710"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.4.1.2"><p id="p7592639101719"><a name="p7592639101719"></a><a name="p7592639101719"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="60%" id="mcps1.2.4.1.3"><p id="p12598123914177"><a name="p12598123914177"></a><a name="p12598123914177"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row6580173917172"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p8603939191714"><a name="p8603939191714"></a><a name="p8603939191714"></a>job_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.2 "><p id="p3608143981713"><a name="p3608143981713"></a><a name="p3608143981713"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p1261303917177"><a name="p1261303917177"></a><a name="p1261303917177"></a>批量增加CN节点任务ID。</p>
</td>
</tr>
</tbody>
</table>

## 请求示例<a name="section156171399178"></a>

```
POST https://{Endpoint}/v1.0/89cd04f168b84af6be287f71730fdb4b/clusters/b5c45780-1006-49e3-b2d5-b3229975bbc7/cns/batch-create

{
  "num" : 3
}
```

## 响应示例<a name="section9647339101714"></a>

**状态码： 200**

批量增加CN节点成功。

```
{
  "job_id" : "2c908185841339ce018414e9944b0020"
}
```

## 状态码<a name="section1867614390176"></a>

<a name="zh-cn_topic_0000001437538225_status_code"></a>
<table><thead align="left"><tr id="row668223913174"><th class="cellrowborder" valign="top" width="15%" id="mcps1.1.3.1.1"><p id="p12689739101713"><a name="p12689739101713"></a><a name="p12689739101713"></a>状态码</p>
</th>
<th class="cellrowborder" valign="top" width="85%" id="mcps1.1.3.1.2"><p id="p669353911715"><a name="p669353911715"></a><a name="p669353911715"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row26821139151716"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p106986390171"><a name="p106986390171"></a><a name="p106986390171"></a>200</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p57039397172"><a name="p57039397172"></a><a name="p57039397172"></a>批量增加CN节点成功。</p>
</td>
</tr>
<tr id="row168216394175"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p37089398174"><a name="p37089398174"></a><a name="p37089398174"></a>400</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p197129391177"><a name="p197129391177"></a><a name="p197129391177"></a>请求错误。</p>
</td>
</tr>
<tr id="row126828398172"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p1716163911714"><a name="p1716163911714"></a><a name="p1716163911714"></a>401</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p77223395170"><a name="p77223395170"></a><a name="p77223395170"></a>鉴权失败。</p>
</td>
</tr>
<tr id="row56823391176"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p1726539151712"><a name="p1726539151712"></a><a name="p1726539151712"></a>403</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p973163910179"><a name="p973163910179"></a><a name="p973163910179"></a>没有操作权限。</p>
</td>
</tr>
<tr id="row206821639151717"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p9736123910179"><a name="p9736123910179"></a><a name="p9736123910179"></a>404</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p117411139161716"><a name="p117411139161716"></a><a name="p117411139161716"></a>找不到资源。</p>
</td>
</tr>
<tr id="row136831139171714"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p97454396172"><a name="p97454396172"></a><a name="p97454396172"></a>500</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p275093910178"><a name="p275093910178"></a><a name="p275093910178"></a>服务内部错误。</p>
</td>
</tr>
<tr id="row1668383981715"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p15754139141715"><a name="p15754139141715"></a><a name="p15754139141715"></a>503</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p107591339181710"><a name="p107591339181710"></a><a name="p107591339181710"></a>服务不可用。</p>
</td>
</tr>
</tbody>
</table>

