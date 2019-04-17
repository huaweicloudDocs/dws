# IAM中创建DWS委托<a name="dws_01_0141"></a>

用户为集群开启审计日志转储功能，将日志数据转储到对象存储服务（Object Storage Service，简称OBS）中，需要通过创建IAM委托授权DWS服务去访问用户的OBS资源。

## 创建委托<a name="section206112523445"></a>

1.  使用注册帐户登录管理控制台。
2.  在“服务列表“中，选择“管理与部署 \> 统一身份认证服务“，进入统一身份认证服务页面。
3.  在左侧导航栏中，单机“委托“，进入“委托“页面。
4.  在“委托“页面，单击“创建委托“。
5.  填选相应的委托信息，单击“确定“。

    **表 1**  创建委托

    <a name="table66133055111910"></a>
    <table><thead align="left"><tr id="row32490906111910"><th class="cellrowborder" valign="top" width="30%" id="mcps1.2.3.1.1"><p id="p14517702111910"><a name="p14517702111910"></a><a name="p14517702111910"></a>参数</p>
    </th>
    <th class="cellrowborder" valign="top" width="70%" id="mcps1.2.3.1.2"><p id="p35083239111910"><a name="p35083239111910"></a><a name="p35083239111910"></a>说明</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row23170149111910"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p64842791111910"><a name="p64842791111910"></a><a name="p64842791111910"></a>委托名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p17774742111910"><a name="p17774742111910"></a><a name="p17774742111910"></a>长度不超过64位，且不可为空。</p>
    </td>
    </tr>
    <tr id="row25754953111910"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p5776486111910"><a name="p5776486111910"></a><a name="p5776486111910"></a>委托类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p65242211111910"><a name="p65242211111910"></a><a name="p65242211111910"></a>必须选择“云服务”。</p>
    </td>
    </tr>
    <tr id="row50308989111910"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p48496302111910"><a name="p48496302111910"></a><a name="p48496302111910"></a>云服务</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p35886355111910"><a name="p35886355111910"></a><a name="p35886355111910"></a>单击“选择”，在“选择云服务”的弹出框中选择“DWS”，单击“确定”。</p>
    </td>
    </tr>
    <tr id="row54541740111910"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p55804859111910"><a name="p55804859111910"></a><a name="p55804859111910"></a>持续时间</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p23899763111910"><a name="p23899763111910"></a><a name="p23899763111910"></a>选择“永久”。</p>
    <div class="note" id="note47354677104651"><a name="note47354677104651"></a><a name="note47354677104651"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p23538910104651"><a name="p23538910104651"></a><a name="p23538910104651"></a>目前仅支持配置为永久，配置其他值可能导致委托授权失败。</p>
    </div></div>
    </td>
    </tr>
    <tr id="row13771277111910"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p41731668111910"><a name="p41731668111910"></a><a name="p41731668111910"></a>描述</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p24821976111910"><a name="p24821976111910"></a><a name="p24821976111910"></a>委托信息，长度为0~255位。</p>
    </td>
    </tr>
    <tr id="row22071196111910"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p238213123015"><a name="p238213123015"></a><a name="p238213123015"></a>权限选择</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p9543077171349"><a name="p9543077171349"></a><a name="p9543077171349"></a>“所属区域”为“全局服务”，“项目”为“对象存储服务”对应的“策略”包含“Tenant Administrator”。</p>
    <p id="p46724365101249"><a name="p46724365101249"></a><a name="p46724365101249"></a>权限修改：单击“操作”列的“修改”，在弹出“策略”对话框。在“可选择策略”中勾选对应策略，单击“确定”。</p>
    <div class="note" id="note58012428112512"><a name="note58012428112512"></a><a name="note58012428112512"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p65485460112517"><a name="p65485460112517"></a><a name="p65485460112517"></a>创建委托完成后无法修改策略。</p>
    </div></div>
    </td>
    </tr>
    </tbody>
    </table>


