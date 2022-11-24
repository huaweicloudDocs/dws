# 查询集群CN节点<a name="ZH-CN_TOPIC_0000001437541653"></a>

## 功能介绍<a name="section128701526151715"></a>

该接口用于查询指定集群的CN节点信息。

## URI<a name="section1879122691710"></a>

```
GET /v1.0/{project_id}/clusters/{cluster_id}/cns
```

**表 1**  路径参数

<a name="table989211261170"></a>
<table><thead align="left"><tr id="row1188662681716"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.1"><p id="p1589410266175"><a name="p1589410266175"></a><a name="p1589410266175"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.2"><p id="p28981526131710"><a name="p28981526131710"></a><a name="p28981526131710"></a>是否必选</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.3"><p id="p18901142610176"><a name="p18901142610176"></a><a name="p18901142610176"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="40%" id="mcps1.2.5.1.4"><p id="p169051226151711"><a name="p169051226151711"></a><a name="p169051226151711"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row98871126131715"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p790813267172"><a name="p790813267172"></a><a name="p790813267172"></a>project_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p891218266170"><a name="p891218266170"></a><a name="p891218266170"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p1916102618172"><a name="p1916102618172"></a><a name="p1916102618172"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p1892082610179"><a name="p1892082610179"></a><a name="p1892082610179"></a>项目ID。获取方法，请参见<a href="获取项目ID.md">获取项目ID</a>。</p>
</td>
</tr>
<tr id="row1388712612173"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p15925626101711"><a name="p15925626101711"></a><a name="p15925626101711"></a>cluster_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p8928132613177"><a name="p8928132613177"></a><a name="p8928132613177"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p15932192631719"><a name="p15932192631719"></a><a name="p15932192631719"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p39351726181710"><a name="p39351726181710"></a><a name="p39351726181710"></a>集群的ID。获取方法，请参见<a href="获取集群ID.md">获取集群ID</a>。</p>
</td>
</tr>
</tbody>
</table>

## 请求参数<a name="section1393812267171"></a>

无

## 响应参数<a name="section59466261175"></a>

**状态码： 200**

**表 2**  响应Body参数

<a name="zh-cn_topic_0000001437418425_response_V1GetCnListResponseBody"></a>
<table><thead align="left"><tr id="row13955182601710"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.4.1.1"><p id="p496113260176"><a name="p496113260176"></a><a name="p496113260176"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.4.1.2"><p id="p109651266176"><a name="p109651266176"></a><a name="p109651266176"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="60%" id="mcps1.2.4.1.3"><p id="p39691426171710"><a name="p39691426171710"></a><a name="p39691426171710"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row2095514268176"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p11973132616171"><a name="p11973132616171"></a><a name="p11973132616171"></a>min_num</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.2 "><p id="p897717267179"><a name="p897717267179"></a><a name="p897717267179"></a>Integer</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p1098111266173"><a name="p1098111266173"></a><a name="p1098111266173"></a>允许的最小CN节点数量。</p>
</td>
</tr>
<tr id="row4955826101718"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p18986192616171"><a name="p18986192616171"></a><a name="p18986192616171"></a>max_num</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.2 "><p id="p1998982615177"><a name="p1998982615177"></a><a name="p1998982615177"></a>Integer</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p10993112691715"><a name="p10993112691715"></a><a name="p10993112691715"></a>允许的最大CN节点数量。</p>
</td>
</tr>
<tr id="row19955122619174"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p699682621711"><a name="p699682621711"></a><a name="p699682621711"></a>instances</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.2 "><p id="p191122718173"><a name="p191122718173"></a><a name="p191122718173"></a>Array of <a href="#zh-cn_topic_0000001437418425_response_V1GetCnListResponseBodyElement">V1GetCnListResponseBodyElement</a> objects</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p115182713172"><a name="p115182713172"></a><a name="p115182713172"></a>CN节点列表。</p>
</td>
</tr>
</tbody>
</table>

**表 3**  V1GetCnListResponseBodyElement

<a name="zh-cn_topic_0000001437418425_response_V1GetCnListResponseBodyElement"></a>
<table><thead align="left"><tr id="row1789278177"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.4.1.1"><p id="p9145274175"><a name="p9145274175"></a><a name="p9145274175"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.4.1.2"><p id="p1118132711173"><a name="p1118132711173"></a><a name="p1118132711173"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="60%" id="mcps1.2.4.1.3"><p id="p2021162751712"><a name="p2021162751712"></a><a name="p2021162751712"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row198122719176"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p3259276178"><a name="p3259276178"></a><a name="p3259276178"></a>id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.2 "><p id="p13294272174"><a name="p13294272174"></a><a name="p13294272174"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p14331277170"><a name="p14331277170"></a><a name="p14331277170"></a>节点ID。</p>
</td>
</tr>
<tr id="row20915276178"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p173652721710"><a name="p173652721710"></a><a name="p173652721710"></a>name</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.2 "><p id="p1440172718177"><a name="p1440172718177"></a><a name="p1440172718177"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p124315270170"><a name="p124315270170"></a><a name="p124315270170"></a>节点名称。</p>
</td>
</tr>
<tr id="row15917276171"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p5481527141715"><a name="p5481527141715"></a><a name="p5481527141715"></a>private_ip</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.2 "><p id="p1651427111710"><a name="p1651427111710"></a><a name="p1651427111710"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p9543276172"><a name="p9543276172"></a><a name="p9543276172"></a>内网IP。</p>
</td>
</tr>
</tbody>
</table>

## 请求示例<a name="section105820271179"></a>

```
GET https://{Endpoint}/v1.0/89cd04f168b84af6be287f71730fdb4b/clusters/4ca46bf1-5c61-48ff-b4f3-0ad4e5e3ba90/cns
```

## 响应示例<a name="section19681027201710"></a>

**状态码： 200**

查询集群CN节点成功。

```
{
  "min_num" : 2,
  "max_num" : 3,
  "instances" : [ {
    "id" : "e07d1bfb-6eac-4827-96e0-d10b8ca29c41",
    "name" : "demo-dws-cn-cn-1-1",
    "private_ip" : "172.16.69.106"
  } ]
}
```

## 状态码<a name="section13112627141716"></a>

<a name="zh-cn_topic_0000001437418425_status_code"></a>
<table><thead align="left"><tr id="row6117162716171"><th class="cellrowborder" valign="top" width="15%" id="mcps1.1.3.1.1"><p id="p10121927101711"><a name="p10121927101711"></a><a name="p10121927101711"></a>状态码</p>
</th>
<th class="cellrowborder" valign="top" width="85%" id="mcps1.1.3.1.2"><p id="p0125827111714"><a name="p0125827111714"></a><a name="p0125827111714"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row181171527141713"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p1612922717179"><a name="p1612922717179"></a><a name="p1612922717179"></a>200</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p1813282718176"><a name="p1813282718176"></a><a name="p1813282718176"></a>查询集群CN节点成功。</p>
</td>
</tr>
<tr id="row211752751720"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p31361278171"><a name="p31361278171"></a><a name="p31361278171"></a>400</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p214012719178"><a name="p214012719178"></a><a name="p214012719178"></a>请求错误。</p>
</td>
</tr>
<tr id="row5117627141718"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p91449278172"><a name="p91449278172"></a><a name="p91449278172"></a>401</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p5147172701717"><a name="p5147172701717"></a><a name="p5147172701717"></a>鉴权失败。</p>
</td>
</tr>
<tr id="row111711274178"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p131501427151711"><a name="p131501427151711"></a><a name="p131501427151711"></a>403</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p18154182710178"><a name="p18154182710178"></a><a name="p18154182710178"></a>没有操作权限。</p>
</td>
</tr>
<tr id="row3117112720172"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p17158427101714"><a name="p17158427101714"></a><a name="p17158427101714"></a>404</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p181623273176"><a name="p181623273176"></a><a name="p181623273176"></a>找不到资源。</p>
</td>
</tr>
<tr id="row411816277176"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p121657275170"><a name="p121657275170"></a><a name="p121657275170"></a>500</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p191692271174"><a name="p191692271174"></a><a name="p191692271174"></a>服务内部错误。</p>
</td>
</tr>
<tr id="row311872701716"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p17173727171711"><a name="p17173727171711"></a><a name="p17173727171711"></a>503</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p16177227111720"><a name="p16177227111720"></a><a name="p16177227111720"></a>服务不可用。</p>
</td>
</tr>
</tbody>
</table>

