# 设置SSL连接<a name="dws_01_0076"></a>

DWS支持SSL认证方式的连接，以加密DWS客户端与数据库之间传输的数据。SSL连接方式的安全性高于普通模式，集群默认开启SSL功能允许来自客户端的SSL连接或非SSL连接，从安全性考虑，建议用户在客户端使用SSL连接方式。如果要强制使用SSL连接，需要为集群开启“服务器端是否强制使用SSL连接“。

在集群的“安全设置“页面可以设置是否开启“服务器端是否强制使用SSL连接“。

>![](public_sys-resources/icon-note.gif) **说明：**   
>-   修改安全配置参数并保存生效可能需要重启集群，将导致集群暂时不可用。  
>-   修改集群安全配置必须同时满足以下两个条件：  
>    -   集群状态为“可用“或“低性能“。  
>    -   任务信息不能处于“创建快照中“、“节点扩容“、“配置中“或“重启中“的状态。  

本章节为您介绍以下内容：

-   [设置SSL连接](#section478703071283)
-   [客户端和服务器端SSL连接参数组合情况](#section1916311515557)

## 设置SSL连接<a name="section478703071283"></a>

1.  通过访问以下地址登录DWS管理控制台：[https://console.huaweicloud.com/dws](https://console.huaweicloud.com/dws)。
2.  单击“集群管理“。
3.  在集群列表中，单击指定集群的名称，然后单击“安全设置“。

    默认显示“配置状态“为“已同步“，表示页面显示的是数据库当前最新结果。

4.  在“SSL连接“区域中，单击“服务器端是否强制使用SSL连接“的设置开关进行设置，建议开启。

    ![](figures/icon_dws_on.png)：为开启，表示服务器端强制要求SSL连接。

    ![](figures/icon_dws_off.jpg)：为关闭，表示服务器端对是否通过SSL连接不作强制要求，默认为关闭。

    **图 1**  SSL连接<a name="fig168181335124718"></a>  
    ![](figures/SSL连接.png "SSL连接")

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   如果使用DWS提供的gsql客户端或ODBC驱动，DWS支持的SSL协议为TLSv1.2。  
    >-   如果使用DWS提供的JDBC驱动，支持的SSL协议有SSLv3、TLSv1、TLSv1.1、TLSv1.2。客户端与数据库之间实际使用何种SSL协议，依赖客户端使用的JDK（Java Development Kit）版本，一般JDK支持多个SSL协议。  

5.  单击“应用“。
6.  在弹出的“保存配置“窗口中，选择是否勾选“立即重启集群“，然后单击“确定“。

    -   如果勾选“立即重启集群“，系统将保存“安全设置“页面的配置并立即重启集群，集群重启成功后安全设置将立即生效。
    -   如果不勾选“立即重启集群“，系统将只保存“安全设置“页面的配置。稍后，用户需要手动重启集群才能使安全设置生效。

    安全设置完成后，在“安全设置“页面，“配置状态“有如下3种状态：

    -   “应用中“：表示系统正在保存配置。
    -   “已同步“：表示配置已保存生效。
    -   “需重启生效“：表示配置已保存但还未生效。如需生效，需重启集群。


## 客户端和服务器端SSL连接参数组合情况<a name="section1916311515557"></a>

客户端最终是否使用SSL加密连接方式、是否验证服务器证书，取决于客户端参数sslmode与服务器端（即DWS集群侧）参数ssl、require\_ssl。参数说明如下：

-   **ssl（服务器）**

    ssl参数表示是否开启SSL功能。on表示开启，off表示关闭。

    -   对于集群版本高于1.3.1（包括1.3.1）的集群，默认为on，不支持在DWS管理控制台上设置。
    -   对于集群版本低于1.3.1的集群，默认为开启，即on。ssl参数可通过DWS管理控制台上集群的“安全设置“页面中的“SSL连接“进行设置。

-   **require\_ssl（服务器）**

    require\_ssl参数是设置服务器端是否强制要求SSL连接，该参数只有当ssl为on时才有效。on表示服务器端强制要求SSL连接。off表示服务器端对是否通过SSL连接不作强制要求。

    -   对于集群版本高于1.3.1（包括1.3.1）的集群，默认为关闭，即off。require\_ssl参数可通过DWS管理控制台上集群的“安全设置“页面中的“服务器端是否强制使用SSL连接“进行设置。
    -   对于集群版本低于1.3.1的集群，默认为off，不支持在DWS管理控制台上设置。

-   **sslmode（客户端）**

    可在SQL客户端工具中进行设置。

    -   在gsql命令行客户端中，就是“PGSSLMODE“参数。
    -   在Data Studio客户端中，就是“SSL模式“参数。


客户端参数sslmode与服务器端参数ssl、require\_ssl配置组合结果如下：

**表 1**  客户端与服务器端SSL参数组合结果

<a name="table15451139114317"></a>
<table><thead align="left"><tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row12708114620112"><th class="cellrowborder" valign="top" width="10.66%" id="mcps1.2.5.1.1"><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1070817460113"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1070817460113"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1070817460113"></a>ssl（服务器）</p>
</th>
<th class="cellrowborder" valign="top" width="14.85%" id="mcps1.2.5.1.2"><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p14708184681118"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p14708184681118"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p14708184681118"></a>sslmode（客户端）</p>
</th>
<th class="cellrowborder" valign="top" width="17.119999999999997%" id="mcps1.2.5.1.3"><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p3709184651116"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p3709184651116"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p3709184651116"></a>require_ssl（服务器）</p>
</th>
<th class="cellrowborder" valign="top" width="57.37%" id="mcps1.2.5.1.4"><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p107096465112"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p107096465112"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p107096465112"></a>结果</p>
</th>
</tr>
</thead>
<tbody><tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row570917468118"><td class="cellrowborder" rowspan="10" valign="top" width="10.66%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p5709124615117"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p5709124615117"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p5709124615117"></a>on</p>
</td>
<td class="cellrowborder" valign="top" width="14.85%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1070914614118"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1070914614118"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1070914614118"></a>disable</p>
</td>
<td class="cellrowborder" valign="top" width="17.119999999999997%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1870974611118"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1870974611118"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1870974611118"></a>on</p>
</td>
<td class="cellrowborder" valign="top" width="57.37%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p2070934661119"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p2070934661119"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p2070934661119"></a>由于服务器端要求使用 SSL，但客户端针对该连接禁用了 SSL，因此无法建立连接。</p>
</td>
</tr>
<tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row670910465110"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p670974621115"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p670974621115"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p670974621115"></a>disable</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p37091646181115"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p37091646181115"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p37091646181115"></a>off</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p970944618110"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p970944618110"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p970944618110"></a>连接未加密。</p>
</td>
</tr>
<tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row17709164615115"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p10710194681119"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p10710194681119"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p10710194681119"></a>allow</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p12710104614113"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p12710104614113"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p12710104614113"></a>on</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p57104469113"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p57104469113"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p57104469113"></a>连接经过加密。</p>
</td>
</tr>
<tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row471064611115"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p19710204641112"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p19710204641112"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p19710204641112"></a>allow</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p67101446141110"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p67101446141110"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p67101446141110"></a>off</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1471074691112"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1471074691112"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1471074691112"></a>连接未加密。</p>
</td>
</tr>
<tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row571024619116"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p17710204641110"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p17710204641110"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p17710204641110"></a>prefer</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p97101746151118"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p97101746151118"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p97101746151118"></a>on</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p10710134651114"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p10710134651114"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p10710134651114"></a>连接经过加密。</p>
</td>
</tr>
<tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row7710154611119"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1671034611112"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1671034611112"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1671034611112"></a>prefer</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p671004621111"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p671004621111"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p671004621111"></a>off</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p77116463115"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p77116463115"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p77116463115"></a>连接经过加密。</p>
</td>
</tr>
<tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row271112468115"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p16711134631110"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p16711134631110"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p16711134631110"></a>require</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p47118467112"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p47118467112"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p47118467112"></a>on</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p7711114619116"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p7711114619116"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p7711114619116"></a>连接经过加密。</p>
</td>
</tr>
<tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row12711154619119"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p67111846101115"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p67111846101115"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p67111846101115"></a>require</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1871116468113"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1871116468113"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1871116468113"></a>off</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p771113462118"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p771113462118"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p771113462118"></a>连接经过加密。</p>
</td>
</tr>
<tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row207111946151110"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p971144691118"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p971144691118"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p971144691118"></a>verify-ca</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p16711164691114"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p16711164691114"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p16711164691114"></a>on</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p2711174615113"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p2711174615113"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p2711174615113"></a>连接经过加密，且验证了服务器证书。</p>
</td>
</tr>
<tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row137110461119"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p57113463117"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p57113463117"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p57113463117"></a>verify-ca</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p167111546151118"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p167111546151118"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p167111546151118"></a>off</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p11711164617113"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p11711164617113"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p11711164617113"></a>连接经过加密，且验证了服务器证书。</p>
</td>
</tr>
<tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row127121746101116"><td class="cellrowborder" rowspan="10" valign="top" width="10.66%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p13712154617114"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p13712154617114"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p13712154617114"></a>off</p>
</td>
<td class="cellrowborder" valign="top" width="14.85%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p137121546111115"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p137121546111115"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p137121546111115"></a>disable</p>
</td>
<td class="cellrowborder" valign="top" width="17.119999999999997%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p13712146161114"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p13712146161114"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p13712146161114"></a>on</p>
</td>
<td class="cellrowborder" valign="top" width="57.37%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p0712124611113"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p0712124611113"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p0712124611113"></a>连接未加密。</p>
</td>
</tr>
<tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row2071214651119"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p15712646161114"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p15712646161114"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p15712646161114"></a>disable</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p47125460116"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p47125460116"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p47125460116"></a>off</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p15712104618119"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p15712104618119"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p15712104618119"></a>连接未加密。</p>
</td>
</tr>
<tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row37121446131114"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1771214612119"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1771214612119"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1771214612119"></a>allow</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1771264611119"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1771264611119"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1771264611119"></a>on</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p11712346201111"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p11712346201111"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p11712346201111"></a>连接未加密。</p>
</td>
</tr>
<tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row10712184610112"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p107131246181111"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p107131246181111"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p107131246181111"></a>allow</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p177138462111"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p177138462111"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p177138462111"></a>off</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p971374671112"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p971374671112"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p971374671112"></a>连接未加密。</p>
</td>
</tr>
<tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row18713846201111"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p14713114618111"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p14713114618111"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p14713114618111"></a>prefer</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p4713154611117"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p4713154611117"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p4713154611117"></a>on</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p2071314691112"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p2071314691112"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p2071314691112"></a>连接未加密。</p>
</td>
</tr>
<tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row971374615115"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p37131446131115"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p37131446131115"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p37131446131115"></a>prefer</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p167135466116"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p167135466116"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p167135466116"></a>off</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p207137465113"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p207137465113"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p207137465113"></a>连接未加密。</p>
</td>
</tr>
<tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row107135467110"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p197131146191113"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p197131146191113"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p197131146191113"></a>require</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p18713846131119"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p18713846131119"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p18713846131119"></a>on</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p7713104619111"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p7713104619111"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p7713104619111"></a>由于客户端要求使用 SSL，但服务器端禁用了 SSL，因此无法建立连接。</p>
</td>
</tr>
<tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row971304620110"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p8713546131119"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p8713546131119"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p8713546131119"></a>require</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p97131946201114"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p97131946201114"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p97131946201114"></a>off</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p37131746161113"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p37131746161113"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p37131746161113"></a>由于客户端要求使用 SSL，但服务器端禁用了 SSL，因此无法建立连接。</p>
</td>
</tr>
<tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row6713104671112"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p37143469110"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p37143469110"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p37143469110"></a>verify-ca</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1071454612117"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1071454612117"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p1071454612117"></a>on</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p671454641116"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p671454641116"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p671454641116"></a>由于客户端要求使用 SSL，但服务器端禁用了 SSL，因此无法建立连接。</p>
</td>
</tr>
<tr id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_row671444611117"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p177141946191116"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p177141946191116"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p177141946191116"></a>verify-ca</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p3714104610115"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p3714104610115"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p3714104610115"></a>off</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p15714546121111"><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p15714546121111"></a><a name="zh-cn_topic_0132455753_zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_p15714546121111"></a>由于客户端要求使用 SSL，但服务器端禁用了 SSL，因此无法建立连接。</p>
</td>
</tr>
</tbody>
</table>

