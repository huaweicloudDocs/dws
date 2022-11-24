# 集群解绑ELB<a name="ZH-CN_TOPIC_0000001387182840"></a>

## 功能介绍<a name="section92078182710"></a>

该接口用于集群解绑ELB。

## URI<a name="section16267819272"></a>

```
DELETE /v2/{project_id}/clusters/{cluster_id}/elbs/{elb_id}
```

**表 1**  路径参数

<a name="table6383822714"></a>
<table><thead align="left"><tr id="row173414818277"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.1"><p id="p4401892712"><a name="p4401892712"></a><a name="p4401892712"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.2"><p id="p14311813272"><a name="p14311813272"></a><a name="p14311813272"></a>是否必选</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.3"><p id="p7469812272"><a name="p7469812272"></a><a name="p7469812272"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="40%" id="mcps1.2.5.1.4"><p id="p0481822712"><a name="p0481822712"></a><a name="p0481822712"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row83512820277"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p1351128132713"><a name="p1351128132713"></a><a name="p1351128132713"></a>project_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p55419852718"><a name="p55419852718"></a><a name="p55419852718"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p16571185274"><a name="p16571185274"></a><a name="p16571185274"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p196098132713"><a name="p196098132713"></a><a name="p196098132713"></a>项目ID。获取方法，请参见<a href="获取项目ID.md">获取项目ID</a>。</p>
</td>
</tr>
<tr id="row53515882718"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p116388142711"><a name="p116388142711"></a><a name="p116388142711"></a>cluster_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p186615814277"><a name="p186615814277"></a><a name="p186615814277"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p4701088275"><a name="p4701088275"></a><a name="p4701088275"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p14731786277"><a name="p14731786277"></a><a name="p14731786277"></a>集群ID。获取方法，请参见<a href="获取集群ID.md">获取集群ID</a>。</p>
</td>
</tr>
<tr id="row103518162712"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p177513818279"><a name="p177513818279"></a><a name="p177513818279"></a>elb_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p778282275"><a name="p778282275"></a><a name="p778282275"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p781158172713"><a name="p781158172713"></a><a name="p781158172713"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p1684158102713"><a name="p1684158102713"></a><a name="p1684158102713"></a>集群已绑定的弹性负载均衡ID。</p>
</td>
</tr>
</tbody>
</table>

## 请求参数<a name="section108616814273"></a>

无

## 响应参数<a name="section1393182270"></a>

**状态码： 200**

**表 2**  响应Body参数

<a name="zh-cn_topic_0000001387179400_response_ElbResponseBody"></a>
<table><thead align="left"><tr id="row11998892716"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.4.1.1"><p id="p101048812270"><a name="p101048812270"></a><a name="p101048812270"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.4.1.2"><p id="p610715810277"><a name="p610715810277"></a><a name="p610715810277"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="60%" id="mcps1.2.4.1.3"><p id="p91109813272"><a name="p91109813272"></a><a name="p91109813272"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row19999817277"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p611310814272"><a name="p611310814272"></a><a name="p611310814272"></a>job_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.2 "><p id="p151168852714"><a name="p151168852714"></a><a name="p151168852714"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p611948182710"><a name="p611948182710"></a><a name="p611948182710"></a>任务ID。</p>
</td>
</tr>
</tbody>
</table>

## 请求示例<a name="section1312238202718"></a>

```
https://{Endpoint}/v2/4cf650fd46704908aa071b4df2453e1e/clusters/194408fa-9d41-435c-a140-91edcf5fe519/elbs/1e6e0b66-6223-4523-bfd9-033c88b4ce9f
```

## 响应示例<a name="section412910815270"></a>

**状态码： 200**

```
{job_id:"2c9081838417d8850184196d8282002b"}
```

## 状态码<a name="section151382892719"></a>

<a name="zh-cn_topic_0000001387179400_status_code"></a>
<table><thead align="left"><tr id="row10142118202716"><th class="cellrowborder" valign="top" width="15%" id="mcps1.1.3.1.1"><p id="p131451988277"><a name="p131451988277"></a><a name="p131451988277"></a>状态码</p>
</th>
<th class="cellrowborder" valign="top" width="85%" id="mcps1.1.3.1.2"><p id="p61481888278"><a name="p61481888278"></a><a name="p61481888278"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row1614219815279"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p1415114811272"><a name="p1415114811272"></a><a name="p1415114811272"></a>200</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p131539872714"><a name="p131539872714"></a><a name="p131539872714"></a>集群解绑ELB成功。</p>
</td>
</tr>
<tr id="row0754193113218"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p167541231112117"><a name="p167541231112117"></a><a name="p167541231112117"></a>400</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p127551431152114"><a name="p127551431152114"></a><a name="p127551431152114"></a>请求错误。</p>
</td>
</tr>
<tr id="row57741234152114"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p377493418215"><a name="p377493418215"></a><a name="p377493418215"></a>401</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p147742034182118"><a name="p147742034182118"></a><a name="p147742034182118"></a>鉴权失败。</p>
</td>
</tr>
<tr id="row10316162922115"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p33171529112114"><a name="p33171529112114"></a><a name="p33171529112114"></a>403</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p1731715292219"><a name="p1731715292219"></a><a name="p1731715292219"></a>没有操作权限。</p>
</td>
</tr>
<tr id="row11803324102117"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p580319244213"><a name="p580319244213"></a><a name="p580319244213"></a>404</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p580382432117"><a name="p580382432117"></a><a name="p580382432117"></a>找不到资源。</p>
</td>
</tr>
<tr id="row31611927172111"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p18161112710213"><a name="p18161112710213"></a><a name="p18161112710213"></a>500</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p1316113277219"><a name="p1316113277219"></a><a name="p1316113277219"></a>服务内部错误。</p>
</td>
</tr>
<tr id="row84031223216"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p1740422211219"><a name="p1740422211219"></a><a name="p1740422211219"></a>503</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p24042227212"><a name="p24042227212"></a><a name="p24042227212"></a>服务不可用。</p>
</td>
</tr>
</tbody>
</table>

