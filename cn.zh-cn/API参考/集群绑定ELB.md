# 集群绑定ELB<a name="ZH-CN_TOPIC_0000001437421901"></a>

## 功能介绍<a name="section10834255142616"></a>

该接口用于集群绑定ELB接口。

## URI<a name="section13839115516262"></a>

```
POST /v2/{project_id}/clusters/{cluster_id}/elbs/{elb_id}
```

**表 1**  路径参数

<a name="table17848125514264"></a>
<table><thead align="left"><tr id="row384455515264"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.1"><p id="p88492558261"><a name="p88492558261"></a><a name="p88492558261"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.2"><p id="p3851175522620"><a name="p3851175522620"></a><a name="p3851175522620"></a>是否必选</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.3"><p id="p3853855102616"><a name="p3853855102616"></a><a name="p3853855102616"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="40%" id="mcps1.2.5.1.4"><p id="p685513553267"><a name="p685513553267"></a><a name="p685513553267"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row2084475511268"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p1285810559261"><a name="p1285810559261"></a><a name="p1285810559261"></a>project_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p1286095517267"><a name="p1286095517267"></a><a name="p1286095517267"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p48621055122617"><a name="p48621055122617"></a><a name="p48621055122617"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p1986445518263"><a name="p1986445518263"></a><a name="p1986445518263"></a>项目ID。获取方法，请参见<a href="获取项目ID.md">获取项目ID</a>。</p>
</td>
</tr>
<tr id="row78451455102616"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p4866355132613"><a name="p4866355132613"></a><a name="p4866355132613"></a>cluster_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p78681555112617"><a name="p78681555112617"></a><a name="p78681555112617"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p2870455142610"><a name="p2870455142610"></a><a name="p2870455142610"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p13872455162610"><a name="p13872455162610"></a><a name="p13872455162610"></a>集群ID。获取方法，请参见<a href="获取集群ID.md">获取集群ID</a>。</p>
</td>
</tr>
<tr id="row14845115522614"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p15875105592613"><a name="p15875105592613"></a><a name="p15875105592613"></a>elb_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p18877195518261"><a name="p18877195518261"></a><a name="p18877195518261"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p178798552267"><a name="p178798552267"></a><a name="p178798552267"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p288125562619"><a name="p288125562619"></a><a name="p288125562619"></a>未绑定的弹性负载均衡ID。</p>
</td>
</tr>
</tbody>
</table>

## 请求参数<a name="section1883755112619"></a>

无

## 响应参数<a name="section7887145552620"></a>

**状态码： 200**

**表 2**  响应Body参数

<a name="zh-cn_topic_0000001437698629_response_ElbResponseBody"></a>
<table><thead align="left"><tr id="row289385517266"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.4.1.1"><p id="p14897135516262"><a name="p14897135516262"></a><a name="p14897135516262"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.4.1.2"><p id="p138996554261"><a name="p138996554261"></a><a name="p138996554261"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="60%" id="mcps1.2.4.1.3"><p id="p189011355152613"><a name="p189011355152613"></a><a name="p189011355152613"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row11893135517264"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p1990385512265"><a name="p1990385512265"></a><a name="p1990385512265"></a>job_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.2 "><p id="p129051755132620"><a name="p129051755132620"></a><a name="p129051755132620"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p15909195502616"><a name="p15909195502616"></a><a name="p15909195502616"></a>任务ID。</p>
</td>
</tr>
</tbody>
</table>

## 请求示例<a name="section129111355152619"></a>

```
https://{Endpoint}/v2/4cf650fd46704908aa071b4df2453e1e/clusters/194408fa-9d41-435c-a140-91edcf5fe519/elbs/1e6e0b66-6223-4523-bfd9-033c88b4ce9f
```

## 响应示例<a name="section59161255132614"></a>

**状态码： 200**

```
{job_id:"2c9081838417d8850184196d8282002b"}
```

## 状态码<a name="section1392365514268"></a>

<a name="zh-cn_topic_0000001437698629_status_code"></a>
<table><thead align="left"><tr id="row16926955202617"><th class="cellrowborder" valign="top" width="15%" id="mcps1.1.3.1.1"><p id="p18928555122616"><a name="p18928555122616"></a><a name="p18928555122616"></a>状态码</p>
</th>
<th class="cellrowborder" valign="top" width="85%" id="mcps1.1.3.1.2"><p id="p793085517263"><a name="p793085517263"></a><a name="p793085517263"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row292695515266"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p18932165552615"><a name="p18932165552615"></a><a name="p18932165552615"></a>200</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p393425513269"><a name="p393425513269"></a><a name="p393425513269"></a>集群绑定ELB成功。</p>
</td>
</tr>
<tr id="row3871333151712"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p14871433191717"><a name="p14871433191717"></a><a name="p14871433191717"></a>400</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p487733141715"><a name="p487733141715"></a><a name="p487733141715"></a>请求错误。</p>
</td>
</tr>
<tr id="row178611935111714"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p886113541716"><a name="p886113541716"></a><a name="p886113541716"></a>401</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p1586233581711"><a name="p1586233581711"></a><a name="p1586233581711"></a>鉴权失败。</p>
</td>
</tr>
<tr id="row17461103811714"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p1461193815172"><a name="p1461193815172"></a><a name="p1461193815172"></a>403</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p3461153841711"><a name="p3461153841711"></a><a name="p3461153841711"></a>没有操作权限。</p>
</td>
</tr>
<tr id="row195024121719"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p795084161719"><a name="p795084161719"></a><a name="p795084161719"></a>404</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p59501941111711"><a name="p59501941111711"></a><a name="p59501941111711"></a>找不到资源。</p>
</td>
</tr>
<tr id="row1210322821716"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p0103192881717"><a name="p0103192881717"></a><a name="p0103192881717"></a>500</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p91031428131716"><a name="p91031428131716"></a><a name="p91031428131716"></a>服务内部错误。</p>
</td>
</tr>
<tr id="row142698255175"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p226962551720"><a name="p226962551720"></a><a name="p226962551720"></a>503</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p8269112541716"><a name="p8269112541716"></a><a name="p8269112541716"></a>服务不可用。</p>
</td>
</tr>
</tbody>
</table>

