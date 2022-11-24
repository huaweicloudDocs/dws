# 获取集群可绑定的ELB列表<a name="ZH-CN_TOPIC_0000001437661649"></a>

## 功能介绍<a name="section1155112547268"></a>

该接口用于查询集群可以关联的ELB列表

## URI<a name="section155566549267"></a>

```
GET /v2/{project_id}/clusters/{cluster_id}/elbs
```

**表 1**  路径参数

<a name="table25641754182617"></a>
<table><thead align="left"><tr id="row125616544268"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.1"><p id="p95651544268"><a name="p95651544268"></a><a name="p95651544268"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.2"><p id="p3567125411265"><a name="p3567125411265"></a><a name="p3567125411265"></a>是否必选</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.3"><p id="p115701554162618"><a name="p115701554162618"></a><a name="p115701554162618"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="40%" id="mcps1.2.5.1.4"><p id="p13572154132613"><a name="p13572154132613"></a><a name="p13572154132613"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row5562165402619"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p1257419541268"><a name="p1257419541268"></a><a name="p1257419541268"></a>project_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p157645412618"><a name="p157645412618"></a><a name="p157645412618"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p857820544266"><a name="p857820544266"></a><a name="p857820544266"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p558085452613"><a name="p558085452613"></a><a name="p558085452613"></a>项目ID。获取方法，请参见<a href="获取项目ID.md">获取项目ID</a>。</p>
</td>
</tr>
<tr id="row13562454192612"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p145831854102618"><a name="p145831854102618"></a><a name="p145831854102618"></a>cluster_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p8585754122618"><a name="p8585754122618"></a><a name="p8585754122618"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p1858795472610"><a name="p1858795472610"></a><a name="p1858795472610"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p1589135419263"><a name="p1589135419263"></a><a name="p1589135419263"></a>集群ID。获取方法，请参见<a href="获取集群ID.md">获取集群ID</a>。</p>
</td>
</tr>
</tbody>
</table>

## 请求参数<a name="section9591254202617"></a>

无

## 响应参数<a name="section1559795412266"></a>

**状态码： 200**

**表 2**  响应Body参数

<a name="zh-cn_topic_0000001387658504_response_ListClusterElbInfo"></a>
<table><thead align="left"><tr id="row760105411268"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.4.1.1"><p id="p116051854102610"><a name="p116051854102610"></a><a name="p116051854102610"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.4.1.2"><p id="p8609115482619"><a name="p8609115482619"></a><a name="p8609115482619"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="60%" id="mcps1.2.4.1.3"><p id="p1261110549267"><a name="p1261110549267"></a><a name="p1261110549267"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row460225482613"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p2614354112619"><a name="p2614354112619"></a><a name="p2614354112619"></a>elbs</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.2 "><p id="p66161454132619"><a name="p66161454132619"></a><a name="p66161454132619"></a>Array of <a href="#zh-cn_topic_0000001387658504_response_ClusterElbInfo">ClusterElbInfo</a> objects</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p5618854162618"><a name="p5618854162618"></a><a name="p5618854162618"></a>弹性负载均衡列表。</p>
</td>
</tr>
</tbody>
</table>

**表 3**  ClusterElbInfo

<a name="zh-cn_topic_0000001387658504_response_ClusterElbInfo"></a>
<table><thead align="left"><tr id="row26211154192616"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.4.1.1"><p id="p106271454172610"><a name="p106271454172610"></a><a name="p106271454172610"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="19.97%" id="mcps1.2.4.1.2"><p id="p4629135482614"><a name="p4629135482614"></a><a name="p4629135482614"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="60.029999999999994%" id="mcps1.2.4.1.3"><p id="p16631195492617"><a name="p16631195492617"></a><a name="p16631195492617"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row1062145411263"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p12633135472615"><a name="p12633135472615"></a><a name="p12633135472615"></a>id</p>
</td>
<td class="cellrowborder" valign="top" width="19.97%" headers="mcps1.2.4.1.2 "><p id="p10635175418267"><a name="p10635175418267"></a><a name="p10635175418267"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60.029999999999994%" headers="mcps1.2.4.1.3 "><p id="p0637554132614"><a name="p0637554132614"></a><a name="p0637554132614"></a>弹性负载均衡ID。</p>
</td>
</tr>
<tr id="row66212541269"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p163955419268"><a name="p163955419268"></a><a name="p163955419268"></a>cluster_id</p>
</td>
<td class="cellrowborder" valign="top" width="19.97%" headers="mcps1.2.4.1.2 "><p id="p86422542264"><a name="p86422542264"></a><a name="p86422542264"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60.029999999999994%" headers="mcps1.2.4.1.3 "><p id="p164415547261"><a name="p164415547261"></a><a name="p164415547261"></a>集群ID。</p>
</td>
</tr>
<tr id="row36221554172620"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p1764617544268"><a name="p1764617544268"></a><a name="p1764617544268"></a>name</p>
</td>
<td class="cellrowborder" valign="top" width="19.97%" headers="mcps1.2.4.1.2 "><p id="p11648185410265"><a name="p11648185410265"></a><a name="p11648185410265"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60.029999999999994%" headers="mcps1.2.4.1.3 "><p id="p14650185422615"><a name="p14650185422615"></a><a name="p14650185422615"></a>弹性负载均衡名称。</p>
</td>
</tr>
<tr id="row19622135419265"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p13652155492619"><a name="p13652155492619"></a><a name="p13652155492619"></a>description</p>
</td>
<td class="cellrowborder" valign="top" width="19.97%" headers="mcps1.2.4.1.2 "><p id="p365425412618"><a name="p365425412618"></a><a name="p365425412618"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60.029999999999994%" headers="mcps1.2.4.1.3 "><p id="p76561854192618"><a name="p76561854192618"></a><a name="p76561854192618"></a>弹性负载均衡描述。</p>
</td>
</tr>
<tr id="row162255417262"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p2066019543269"><a name="p2066019543269"></a><a name="p2066019543269"></a>vip_address</p>
</td>
<td class="cellrowborder" valign="top" width="19.97%" headers="mcps1.2.4.1.2 "><p id="p3662185418268"><a name="p3662185418268"></a><a name="p3662185418268"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60.029999999999994%" headers="mcps1.2.4.1.3 "><p id="p16665195411260"><a name="p16665195411260"></a><a name="p16665195411260"></a>弹性负载均衡地址。</p>
</td>
</tr>
<tr id="row15622175492613"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p11666554142617"><a name="p11666554142617"></a><a name="p11666554142617"></a>vip_subnet_id</p>
</td>
<td class="cellrowborder" valign="top" width="19.97%" headers="mcps1.2.4.1.2 "><p id="p266805462615"><a name="p266805462615"></a><a name="p266805462615"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60.029999999999994%" headers="mcps1.2.4.1.3 "><p id="p6670125412266"><a name="p6670125412266"></a><a name="p6670125412266"></a>子网ID。</p>
</td>
</tr>
<tr id="row2622145432611"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p17674155482610"><a name="p17674155482610"></a><a name="p17674155482610"></a>tenant_id</p>
</td>
<td class="cellrowborder" valign="top" width="19.97%" headers="mcps1.2.4.1.2 "><p id="p7676155422619"><a name="p7676155422619"></a><a name="p7676155422619"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60.029999999999994%" headers="mcps1.2.4.1.3 "><p id="p1067955416265"><a name="p1067955416265"></a><a name="p1067955416265"></a>租户ID。</p>
</td>
</tr>
<tr id="row1262285413269"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p186811854132615"><a name="p186811854132615"></a><a name="p186811854132615"></a>type</p>
</td>
<td class="cellrowborder" valign="top" width="19.97%" headers="mcps1.2.4.1.2 "><p id="p1368395452614"><a name="p1368395452614"></a><a name="p1368395452614"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60.029999999999994%" headers="mcps1.2.4.1.3 "><p id="p147061491300"><a name="p147061491300"></a><a name="p147061491300"></a>弹性负载均衡类型。其中包括：</p>
<a name="ul13989132123014"></a><a name="ul13989132123014"></a><ul id="ul13989132123014"><li>Internal</li><li>External</li></ul>
<p id="p126861454182613"><a name="p126861454182613"></a><a name="p126861454182613"></a></p>
</td>
</tr>
<tr id="row14623165414267"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p1688125411264"><a name="p1688125411264"></a><a name="p1688125411264"></a>admin_state_up</p>
</td>
<td class="cellrowborder" valign="top" width="19.97%" headers="mcps1.2.4.1.2 "><p id="p1669110546267"><a name="p1669110546267"></a><a name="p1669110546267"></a>Boolean</p>
</td>
<td class="cellrowborder" valign="top" width="60.029999999999994%" headers="mcps1.2.4.1.3 "><p id="p76321424183011"><a name="p76321424183011"></a><a name="p76321424183011"></a>弹性负载均衡的管理状态。其中包括：</p>
<a name="ul5267134017305"></a><a name="ul5267134017305"></a><ul id="ul5267134017305"><li>ACTIVE</li><li>PENDING_CREATE</li><li>ERROR</li></ul>
<p id="p669416544260"><a name="p669416544260"></a><a name="p669416544260"></a></p>
</td>
</tr>
<tr id="row146231854152616"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p166961754102619"><a name="p166961754102619"></a><a name="p166961754102619"></a>bandwidth</p>
</td>
<td class="cellrowborder" valign="top" width="19.97%" headers="mcps1.2.4.1.2 "><p id="p106981654142614"><a name="p106981654142614"></a><a name="p106981654142614"></a>Integer</p>
</td>
<td class="cellrowborder" valign="top" width="60.029999999999994%" headers="mcps1.2.4.1.3 "><p id="p159631543143113"><a name="p159631543143113"></a><a name="p159631543143113"></a>绑定状态：</p>
<a name="ul36121556123110"></a><a name="ul36121556123110"></a><ul id="ul36121556123110"><li>0为未绑定</li><li>1为已绑定</li></ul>
<p id="p167009548267"><a name="p167009548267"></a><a name="p167009548267"></a></p>
</td>
</tr>
<tr id="row16623154122619"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p0703155432620"><a name="p0703155432620"></a><a name="p0703155432620"></a>vpc_id</p>
</td>
<td class="cellrowborder" valign="top" width="19.97%" headers="mcps1.2.4.1.2 "><p id="p770618547268"><a name="p770618547268"></a><a name="p770618547268"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60.029999999999994%" headers="mcps1.2.4.1.3 "><p id="p6708554102620"><a name="p6708554102620"></a><a name="p6708554102620"></a>虚拟私有云ID。</p>
</td>
</tr>
</tbody>
</table>

## 请求示例<a name="section1071095413264"></a>

```
GET https://{Endpoint}/v2/4cf650fd46704908aa071b4df2453e1e/clusters/194408fa-9d41-435c-a140-91edcf5fe519/elbs
```

## 响应示例<a name="section1271518548264"></a>

**状态码： 200**

弹性负载均衡列表

```
{
  "elbs" : [ {
    "id" : "1e6e0b66-6223-4523-bfd9-033c88b4ce9f",
    "name" : "loadbalancer5",
    "description" : "simple lb",
    "bandwidth" : 0,
    "vip_address" : "192.168.0.222",
    "admin_state_up" : true,
    "vpc_id" : "c9f1171e-dc90-4ae9-bf22-f9736983ce2d"
  } ]
}
```

## 状态码<a name="section474112544264"></a>

<a name="zh-cn_topic_0000001387658504_status_code"></a>
<table><thead align="left"><tr id="row177442054162617"><th class="cellrowborder" valign="top" width="14.979999999999999%" id="mcps1.1.3.1.1"><p id="p474655462613"><a name="p474655462613"></a><a name="p474655462613"></a>状态码</p>
</th>
<th class="cellrowborder" valign="top" width="85.02%" id="mcps1.1.3.1.2"><p id="p77481654142616"><a name="p77481654142616"></a><a name="p77481654142616"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row474485412266"><td class="cellrowborder" valign="top" width="14.979999999999999%" headers="mcps1.1.3.1.1 "><p id="p1575017543263"><a name="p1575017543263"></a><a name="p1575017543263"></a>200</p>
</td>
<td class="cellrowborder" valign="top" width="85.02%" headers="mcps1.1.3.1.2 "><p id="p3753165419263"><a name="p3753165419263"></a><a name="p3753165419263"></a>获取弹性负载均衡列表成功。</p>
</td>
</tr>
<tr id="row1802126192011"><td class="cellrowborder" valign="top" width="14.979999999999999%" headers="mcps1.1.3.1.1 "><p id="p080213622019"><a name="p080213622019"></a><a name="p080213622019"></a>400</p>
</td>
<td class="cellrowborder" valign="top" width="85.02%" headers="mcps1.1.3.1.2 "><p id="p1080219614204"><a name="p1080219614204"></a><a name="p1080219614204"></a>请求错误。</p>
</td>
</tr>
<tr id="row813318919208"><td class="cellrowborder" valign="top" width="14.979999999999999%" headers="mcps1.1.3.1.1 "><p id="p1713315915209"><a name="p1713315915209"></a><a name="p1713315915209"></a>401</p>
</td>
<td class="cellrowborder" valign="top" width="85.02%" headers="mcps1.1.3.1.2 "><p id="p1613317932014"><a name="p1613317932014"></a><a name="p1613317932014"></a>鉴权失败。</p>
</td>
</tr>
<tr id="row695515112014"><td class="cellrowborder" valign="top" width="14.979999999999999%" headers="mcps1.1.3.1.1 "><p id="p195515112018"><a name="p195515112018"></a><a name="p195515112018"></a>403</p>
</td>
<td class="cellrowborder" valign="top" width="85.02%" headers="mcps1.1.3.1.2 "><p id="p17955181122014"><a name="p17955181122014"></a><a name="p17955181122014"></a>没有操作权限。</p>
</td>
</tr>
<tr id="row1989851111206"><td class="cellrowborder" valign="top" width="14.979999999999999%" headers="mcps1.1.3.1.1 "><p id="p489871162015"><a name="p489871162015"></a><a name="p489871162015"></a>404</p>
</td>
<td class="cellrowborder" valign="top" width="85.02%" headers="mcps1.1.3.1.2 "><p id="p19898101192014"><a name="p19898101192014"></a><a name="p19898101192014"></a>找不到资源。</p>
</td>
</tr>
<tr id="row14267346209"><td class="cellrowborder" valign="top" width="14.979999999999999%" headers="mcps1.1.3.1.1 "><p id="p20267104192019"><a name="p20267104192019"></a><a name="p20267104192019"></a>500</p>
</td>
<td class="cellrowborder" valign="top" width="85.02%" headers="mcps1.1.3.1.2 "><p id="p142679413207"><a name="p142679413207"></a><a name="p142679413207"></a>服务内部错误。</p>
</td>
</tr>
<tr id="row867415593195"><td class="cellrowborder" valign="top" width="14.979999999999999%" headers="mcps1.1.3.1.1 "><p id="p176747599199"><a name="p176747599199"></a><a name="p176747599199"></a>503</p>
</td>
<td class="cellrowborder" valign="top" width="85.02%" headers="mcps1.1.3.1.2 "><p id="p14674155941915"><a name="p14674155941915"></a><a name="p14674155941915"></a>服务不可用。</p>
</td>
</tr>
</tbody>
</table>

