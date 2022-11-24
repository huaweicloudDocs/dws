# 查询job进度<a name="ZH-CN_TOPIC_0000001448850739"></a>

## 功能介绍<a name="section17449172618583"></a>

该接口用于查询job进度信息。

## URI<a name="section16451152610581"></a>

```
GET /v1.0/{project_id}/job/{job_id}
```

**表 1**  路径参数

<a name="table11455112685818"></a>
<table><thead align="left"><tr id="row18453926165816"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.1"><p id="p12456192685814"><a name="p12456192685814"></a><a name="p12456192685814"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.2"><p id="p6457102695820"><a name="p6457102695820"></a><a name="p6457102695820"></a>是否必选</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.5.1.3"><p id="p184601626175817"><a name="p184601626175817"></a><a name="p184601626175817"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="40%" id="mcps1.2.5.1.4"><p id="p2046142685818"><a name="p2046142685818"></a><a name="p2046142685818"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row945352618587"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p11462162635818"><a name="p11462162635818"></a><a name="p11462162635818"></a>project_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p124636261589"><a name="p124636261589"></a><a name="p124636261589"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p34650264585"><a name="p34650264585"></a><a name="p34650264585"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p124661126185816"><a name="p124661126185816"></a><a name="p124661126185816"></a>项目ID。获取方法，请参见<a href="获取项目ID.md">获取项目ID</a>。</p>
</td>
</tr>
<tr id="row445442616587"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.1 "><p id="p16467726155818"><a name="p16467726155818"></a><a name="p16467726155818"></a>job_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.2 "><p id="p246822645810"><a name="p246822645810"></a><a name="p246822645810"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.5.1.3 "><p id="p18470172655819"><a name="p18470172655819"></a><a name="p18470172655819"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.5.1.4 "><p id="p3471182612581"><a name="p3471182612581"></a><a name="p3471182612581"></a>任务ID。</p>
</td>
</tr>
</tbody>
</table>

## 请求参数<a name="section1647219263584"></a>

无

## 响应参数<a name="section847612614587"></a>

**状态码： 200**

**表 2**  响应Body参数

<a name="zh-cn_topic_0000001448688385_response_JobInfoResp"></a>
<table><thead align="left"><tr id="row14480172645816"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.4.1.1"><p id="p104841626145811"><a name="p104841626145811"></a><a name="p104841626145811"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="20%" id="mcps1.2.4.1.2"><p id="p7485112617582"><a name="p7485112617582"></a><a name="p7485112617582"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="60%" id="mcps1.2.4.1.3"><p id="p9486126165818"><a name="p9486126165818"></a><a name="p9486126165818"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row84810265589"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p20488426105812"><a name="p20488426105812"></a><a name="p20488426105812"></a>job_id</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.2 "><p id="p149112625817"><a name="p149112625817"></a><a name="p149112625817"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p2492726145818"><a name="p2492726145818"></a><a name="p2492726145818"></a>任务ID。</p>
</td>
</tr>
<tr id="row34811126115816"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p134941826195810"><a name="p134941826195810"></a><a name="p134941826195810"></a>job_name</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.2 "><p id="p2495162675816"><a name="p2495162675816"></a><a name="p2495162675816"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p6496226125819"><a name="p6496226125819"></a><a name="p6496226125819"></a>任务名称。</p>
</td>
</tr>
<tr id="row174811326195817"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p124971726115819"><a name="p124971726115819"></a><a name="p124971726115819"></a>begin_time</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.2 "><p id="p1349812269584"><a name="p1349812269584"></a><a name="p1349812269584"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p16499172615819"><a name="p16499172615819"></a><a name="p16499172615819"></a>任务开始时间。</p>
</td>
</tr>
<tr id="row348122611581"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p150082675817"><a name="p150082675817"></a><a name="p150082675817"></a>end_time</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.2 "><p id="p14501926105816"><a name="p14501926105816"></a><a name="p14501926105816"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p8502132655811"><a name="p8502132655811"></a><a name="p8502132655811"></a>任务结束时间。</p>
</td>
</tr>
<tr id="row8481102635812"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p1550318265583"><a name="p1550318265583"></a><a name="p1550318265583"></a>status</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.2 "><p id="p95059268589"><a name="p95059268589"></a><a name="p95059268589"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p1050611263586"><a name="p1050611263586"></a><a name="p1050611263586"></a>任务当前状态。</p>
</td>
</tr>
<tr id="row848182635813"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p75072268587"><a name="p75072268587"></a><a name="p75072268587"></a>failed_code</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.2 "><p id="p15081826155813"><a name="p15081826155813"></a><a name="p15081826155813"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p1450932695816"><a name="p1450932695816"></a><a name="p1450932695816"></a>任务失败错误码。</p>
</td>
</tr>
<tr id="row1848232617583"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p1651032655813"><a name="p1651032655813"></a><a name="p1651032655813"></a>failed_detail</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.2 "><p id="p151217263583"><a name="p151217263583"></a><a name="p151217263583"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p151362612584"><a name="p151362612584"></a><a name="p151362612584"></a>任务失败错误详情。</p>
</td>
</tr>
<tr id="row2482826105815"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.1 "><p id="p17514126105812"><a name="p17514126105812"></a><a name="p17514126105812"></a>progress</p>
</td>
<td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.4.1.2 "><p id="p18515162675815"><a name="p18515162675815"></a><a name="p18515162675815"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p17516726145816"><a name="p17516726145816"></a><a name="p17516726145816"></a>任务进度。</p>
</td>
</tr>
</tbody>
</table>

## 请求示例<a name="section155171526135818"></a>

```
https://{Endpoint}/v1.0/05f2cff45100d5112f4bc00b794ea08e/job/2c9080e8845b207101845b245e1e0001
```

## 响应示例<a name="section0519326205819"></a>

**状态码： 200**

任务进度

```
{
  "status" : "FAIL",
  "progress" : "9%",
  "job_id" : "2c9080e88459fa44018459fbeb600001",
  "job_name" : "ecfClusterElbCreateJob",
  "begin_time" : "2022-11-09T20:25:00",
  "end_time" : "2022-11-09T20:30:00",
  "failed_code" : "CreateELBTask-fail:DWS.0114",
  "failed_detail" : "DWS.0114:ELB private IP is not configured."
}
```

## 状态码<a name="section7531182611586"></a>

<a name="zh-cn_topic_0000001448688385_status_code"></a>
<table><thead align="left"><tr id="row17533122613584"><th class="cellrowborder" valign="top" width="15%" id="mcps1.1.3.1.1"><p id="p1353815261582"><a name="p1353815261582"></a><a name="p1353815261582"></a>状态码</p>
</th>
<th class="cellrowborder" valign="top" width="85%" id="mcps1.1.3.1.2"><p id="p1953918265584"><a name="p1953918265584"></a><a name="p1953918265584"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row9533112655814"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p1540926185819"><a name="p1540926185819"></a><a name="p1540926185819"></a>200</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p35412026175814"><a name="p35412026175814"></a><a name="p35412026175814"></a>查询任务进度成功。</p>
</td>
</tr>
<tr id="row95338266584"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p11542112614583"><a name="p11542112614583"></a><a name="p11542112614583"></a>400</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p2054313267580"><a name="p2054313267580"></a><a name="p2054313267580"></a>请求错误。</p>
</td>
</tr>
<tr id="row2053352619583"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p85441126195814"><a name="p85441126195814"></a><a name="p85441126195814"></a>401</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p15545112655818"><a name="p15545112655818"></a><a name="p15545112655818"></a>鉴权失败。</p>
</td>
</tr>
<tr id="row20533102665816"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p5547132685815"><a name="p5547132685815"></a><a name="p5547132685815"></a>403</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p13548926135810"><a name="p13548926135810"></a><a name="p13548926135810"></a>没有操作权限。</p>
</td>
</tr>
<tr id="row1653492655811"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p15492026155812"><a name="p15492026155812"></a><a name="p15492026155812"></a>404</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p35532264589"><a name="p35532264589"></a><a name="p35532264589"></a>找不到资源。</p>
</td>
</tr>
<tr id="row165341126205814"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p195551426145817"><a name="p195551426145817"></a><a name="p195551426145817"></a>500</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p055612266588"><a name="p055612266588"></a><a name="p055612266588"></a>服务内部错误。</p>
</td>
</tr>
<tr id="row10534126115819"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.1.3.1.1 "><p id="p35571726185812"><a name="p35571726185812"></a><a name="p35571726185812"></a>503</p>
</td>
<td class="cellrowborder" valign="top" width="85%" headers="mcps1.1.3.1.2 "><p id="p3558926195810"><a name="p3558926195810"></a><a name="p3558926195810"></a>服务不可用。</p>
</td>
</tr>
</tbody>
</table>

