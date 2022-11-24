# 批量删除CN节点<a name="ZH-CN_TOPIC_0000001387501956"></a>

## 功能介绍<a name="section205814500177"></a>

该接口用于为指定集群删除CN节点。

## URI<a name="section571205031711"></a>

```
POST /v1.0/{project_id}/clusters/{cluster_id}/cns/batch-delete
```

**表 1**  路径参数

<a name="table1691135010174"></a>
<table><thead align="left"><tr id="row108417504179"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.1"><p id="p1951250181719"><a name="p1951250181719"></a><a name="p1951250181719"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.2"><p id="p10101145020175"><a name="p10101145020175"></a><a name="p10101145020175"></a>是否必选</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.3"><p id="p110835031713"><a name="p110835031713"></a><a name="p110835031713"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="40%" id="mcps1.2.5.1.4"><p id="p61149506176"><a name="p61149506176"></a><a name="p61149506176"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row208425081711"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p1212035081717"><a name="p1212035081717"></a><a name="p1212035081717"></a>project_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p1612695012177"><a name="p1612695012177"></a><a name="p1612695012177"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p111331050121719"><a name="p111331050121719"></a><a name="p111331050121719"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p12139145013173"><a name="p12139145013173"></a><a name="p12139145013173"></a>项目ID。获取方法，请参见<a href="获取项目ID.md">获取项目ID</a>。</p>
</td>
</tr>
<tr id="row2851450131716"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p16145150181718"><a name="p16145150181718"></a><a name="p16145150181718"></a>cluster_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p121501450131713"><a name="p121501450131713"></a><a name="p121501450131713"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p10156250101717"><a name="p10156250101717"></a><a name="p10156250101717"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p71631250121719"><a name="p71631250121719"></a><a name="p71631250121719"></a>集群的ID。获取方法，请参见<a href="获取集群ID.md">获取集群ID</a>。</p>
</td>
</tr>
</tbody>
</table>

## 请求参数<a name="section2017016503176"></a>

**表 2**  请求Body参数

<a name="zh-cn_topic_0000001437658181_request_V1BatchDeleteCnRequestBody"></a>
<table><thead align="left"><tr id="row71771350101712"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.1"><p id="p1918745012172"><a name="p1918745012172"></a><a name="p1918745012172"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.2"><p id="p201934504178"><a name="p201934504178"></a><a name="p201934504178"></a>是否必选</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.3"><p id="p320011501179"><a name="p320011501179"></a><a name="p320011501179"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="40%" id="mcps1.2.5.1.4"><p id="p32061750181720"><a name="p32061750181720"></a><a name="p32061750181720"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row1317818509172"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p621295017176"><a name="p621295017176"></a><a name="p621295017176"></a>instances</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p7218185011715"><a name="p7218185011715"></a><a name="p7218185011715"></a>否</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p17225550141719"><a name="p17225550141719"></a><a name="p17225550141719"></a>Array of strings</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p1823125017175"><a name="p1823125017175"></a><a name="p1823125017175"></a>批量删除CN节点ID。</p>
</td>
</tr>
</tbody>
</table>

## 响应参数<a name="section2238550201720"></a>

**状态码： 200**

**表 3**  响应Body参数

<a name="zh-cn_topic_0000001437658181_response_V1BatchDeleteCnResponseBody"></a>
<table><thead align="left"><tr id="row1725045071720"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.4.1.1"><p id="p10260105051719"><a name="p10260105051719"></a><a name="p10260105051719"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.4.1.2"><p id="p20266155019173"><a name="p20266155019173"></a><a name="p20266155019173"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="60%" id="mcps1.2.4.1.3"><p id="p202722050151716"><a name="p202722050151716"></a><a name="p202722050151716"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row1250950131718"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p172781450141711"><a name="p172781450141711"></a><a name="p172781450141711"></a>job_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.2 "><p id="p2285115091719"><a name="p2285115091719"></a><a name="p2285115091719"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p1529115015179"><a name="p1529115015179"></a><a name="p1529115015179"></a>批量删除CN节点任务ID。</p>
</td>
</tr>
</tbody>
</table>

## 请求示例<a name="section132971250101713"></a>

```
POST https://{Endpoint}/v1.0/89cd04f168b84af6be287f71730fdb4b/clusters/b5c45780-1006-49e3-b2d5-b3229975bbc7/cns/batch-delete

{
  "instances" : [ "b6ad3dc3-d2de-4d2c-a5df-fdde58eca8f0" ]
}
```

## 响应示例<a name="section533505012176"></a>

**状态码： 200**

批量删除CN节点成功。

```
{
  "job_id" : "2c908185841339ce018414e9944b0020"
}
```

## 状态码<a name="section1372165010173"></a>

<a name="zh-cn_topic_0000001437658181_status_code"></a>
<table><thead align="left"><tr id="row937910504173"><th class="cellrowborder" valign="top" width="15%" id="mcps1.1.3.1.1"><p id="p1938615012172"><a name="p1938615012172"></a><a name="p1938615012172"></a>状态码</p>
</th>
<th class="cellrowborder" valign="top" width="85%" id="mcps1.1.3.1.2"><p id="p12393205041720"><a name="p12393205041720"></a><a name="p12393205041720"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row6380115041711"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p5398250191712"><a name="p5398250191712"></a><a name="p5398250191712"></a>200</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p740315010176"><a name="p740315010176"></a><a name="p740315010176"></a>批量删除CN节点成功。</p>
</td>
</tr>
<tr id="row238045001718"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p541013504179"><a name="p541013504179"></a><a name="p541013504179"></a>400</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p2416550171716"><a name="p2416550171716"></a><a name="p2416550171716"></a>请求错误。</p>
</td>
</tr>
<tr id="row5380250181715"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p34221507172"><a name="p34221507172"></a><a name="p34221507172"></a>401</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p9428050181714"><a name="p9428050181714"></a><a name="p9428050181714"></a>鉴权失败。</p>
</td>
</tr>
<tr id="row203801650181716"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p2434195091710"><a name="p2434195091710"></a><a name="p2434195091710"></a>403</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p114401050111718"><a name="p114401050111718"></a><a name="p114401050111718"></a>没有操作权限。</p>
</td>
</tr>
<tr id="row20380185015176"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p9446105012175"><a name="p9446105012175"></a><a name="p9446105012175"></a>404</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p3452125015174"><a name="p3452125015174"></a><a name="p3452125015174"></a>找不到资源。</p>
</td>
</tr>
<tr id="row0380105091710"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p7459165021714"><a name="p7459165021714"></a><a name="p7459165021714"></a>500</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p1946517507172"><a name="p1946517507172"></a><a name="p1946517507172"></a>服务内部错误。</p>
</td>
</tr>
<tr id="row038145015175"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p2471950131714"><a name="p2471950131714"></a><a name="p2471950131714"></a>503</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p1347619503174"><a name="p1347619503174"></a><a name="p1347619503174"></a>服务不可用。</p>
</td>
</tr>
</tbody>
</table>

