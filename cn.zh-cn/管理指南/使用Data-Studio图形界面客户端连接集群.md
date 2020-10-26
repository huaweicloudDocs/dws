# 使用Data Studio图形界面客户端连接集群<a name="dws_01_0094"></a>

Data Studio是一款运行在Windows操作系统上的SQL客户端工具，有着丰富的GUI界面，能够管理数据库和数据库对象，编辑、运行、调试SQL脚本，查看执行计划等。在GaussDB\(DWS\) 管理控制台下载Data Studio软件包，解压后免安装即可使用。

DataStudio可供下载的版本分为“Windows x86“和“Windows x64“两种版本，分别支持32位和64位Windows操作系统。

## 连接集群前的准备<a name="section83156195500"></a>

-   GaussDB\(DWS\) 集群已绑定弹性IP。
-   已获取GaussDB\(DWS\) 集群的数据库管理员用户名和密码。
-   已获取GaussDB\(DWS\) 集群的公网访问地址，含IP地址和端口。具体请参见[获取集群连接地址](获取集群连接地址.md)。
-   已配置GaussDB\(DWS\) 集群所属的安全组，添加入规则允许用户的IP地址使用TCP访问端口。

    具体步骤，请参见《虚拟私有云用户指南》中的[添加安全组规则](https://support.huaweicloud.com/usermanual-vpc/zh-cn_topic_0030969470.html)章节。


## 使用Data Studio连接到集群数据库<a name="section12757151571018"></a>

1.  GaussDB\(DWS\) 提供了基于Windows平台的Data Studio图形界面客户端，该工具依赖JDK，请先在客户端主机上安装Java 1.8.0\_141或以上版本的JDK，但是只支持java8版本。

    在Windows操作系统中，您可以访问[JDK官网](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)，下载符合操作系统版本的JDK，并根据指导进行安装。

2.  登录GaussDB\(DWS\) 管理控制台。
3.  单击“连接管理“。
4.  在“下载客户端和驱动“页面，下载“Data Studio图形界面客户端“。

    -   请根据操作系统类型，选择“Windows x86“或“Windows x64“，再单击“下载“，可以下载与现有集群版本匹配的Data Studio工具。

        如果同时拥有不同版本的集群，单击“下载”时会下载与集群最低版本相对应的Data Studio工具。如果当前没有集群，单击“下载”时将下载到低版本的Data Studio工具。GaussDB\(DWS\) 集群可向下兼容低版本的Data Studio工具。

    -   单击“历史版本”可根据集群版本下载相应版本的Data Studio工具，建议按集群版本下载配套的工具。

    **图 1**  下载客户端<a name="zh-cn_topic_0107187019_fig68962081218"></a>  
    ![](figures/下载客户端.png "下载客户端")

    如果同时拥有不同版本的集群，系统会弹出对话框，提示您选择“集群版本“然后下载与集群版本相对应的客户端。在“集群管理“页面的集群列表中，单击指定集群的名称，再选择“基本信息“页签，可查看集群版本。

5.  解压下载的客户端软件包（32位或64位）到需要安装的路径。
6.  打开安装目录，双击Data Studio.exe，启动Data Studio客户端，如[图2](#zh-cn_topic_0107187019_fig6324139192412)所示。

    **图 2**  启动客户端<a name="zh-cn_topic_0107187019_fig6324139192412"></a>  
    ![](figures/启动客户端.png "启动客户端")

7.  在主菜单中选择“文件“  \>  “新建连接“，如[图3](#zh-cn_topic_0107187019_fig14311312192811)所示。

    **图 3**  新建连接<a name="zh-cn_topic_0107187019_fig14311312192811"></a>  
    ![](figures/新建连接.png "新建连接")

8.  在弹出的“新建/选择数据库连接“页面中，如下图所示，输入连接参数。

    **图 4**  配置连接参数<a name="zh-cn_topic_0107187019_fig27101723910"></a>  
    ![](figures/配置连接参数.png "配置连接参数")

    **表 1**  配置连接参数

    <a name="zh-cn_topic_0107187019_table79217143912"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0107187019_row88417113910"><th class="cellrowborder" valign="top" width="19.01190119011901%" id="mcps1.2.4.1.1"><p id="zh-cn_topic_0107187019_p167171710393"><a name="zh-cn_topic_0107187019_p167171710393"></a><a name="zh-cn_topic_0107187019_p167171710393"></a>字段名称</p>
    </th>
    <th class="cellrowborder" valign="top" width="58.8058805880588%" id="mcps1.2.4.1.2"><p id="zh-cn_topic_0107187019_p9741716392"><a name="zh-cn_topic_0107187019_p9741716392"></a><a name="zh-cn_topic_0107187019_p9741716392"></a>说明</p>
    </th>
    <th class="cellrowborder" valign="top" width="22.182218221822183%" id="mcps1.2.4.1.3"><p id="zh-cn_topic_0107187019_p88171713915"><a name="zh-cn_topic_0107187019_p88171713915"></a><a name="zh-cn_topic_0107187019_p88171713915"></a>举例</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0107187019_row1816716134011"><td class="cellrowborder" valign="top" width="19.01190119011901%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0107187019_p51683131702"><a name="zh-cn_topic_0107187019_p51683131702"></a><a name="zh-cn_topic_0107187019_p51683131702"></a>数据库类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.8058805880588%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0107187019_p3297172210156"><a name="zh-cn_topic_0107187019_p3297172210156"></a><a name="zh-cn_topic_0107187019_p3297172210156"></a>选择“GaussDB(DWS) ”。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.182218221822183%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0107187019_p916914138012"><a name="zh-cn_topic_0107187019_p916914138012"></a><a name="zh-cn_topic_0107187019_p916914138012"></a>GaussDB(DWS)</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0107187019_row138017153913"><td class="cellrowborder" valign="top" width="19.01190119011901%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0107187019_p38131716399"><a name="zh-cn_topic_0107187019_p38131716399"></a><a name="zh-cn_topic_0107187019_p38131716399"></a>名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.8058805880588%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0107187019_p7813171399"><a name="zh-cn_topic_0107187019_p7813171399"></a><a name="zh-cn_topic_0107187019_p7813171399"></a>连接名称。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.182218221822183%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0107187019_p11813172392"><a name="zh-cn_topic_0107187019_p11813172392"></a><a name="zh-cn_topic_0107187019_p11813172392"></a>dws-demo</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0107187019_row178141710395"><td class="cellrowborder" valign="top" width="19.01190119011901%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0107187019_p12812176393"><a name="zh-cn_topic_0107187019_p12812176393"></a><a name="zh-cn_topic_0107187019_p12812176393"></a>主机名</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.8058805880588%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0107187019_p38191720395"><a name="zh-cn_topic_0107187019_p38191720395"></a><a name="zh-cn_topic_0107187019_p38191720395"></a>所要连接的集群IP地址（IPv4）或域名。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.182218221822183%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0107187019_p88617143914"><a name="zh-cn_topic_0107187019_p88617143914"></a><a name="zh-cn_topic_0107187019_p88617143914"></a>-</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0107187019_row88151717394"><td class="cellrowborder" valign="top" width="19.01190119011901%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0107187019_p88017123920"><a name="zh-cn_topic_0107187019_p88017123920"></a><a name="zh-cn_topic_0107187019_p88017123920"></a>端口号</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.8058805880588%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0107187019_p2861717396"><a name="zh-cn_topic_0107187019_p2861717396"></a><a name="zh-cn_topic_0107187019_p2861717396"></a>端口地址。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.182218221822183%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0107187019_p3812176392"><a name="zh-cn_topic_0107187019_p3812176392"></a><a name="zh-cn_topic_0107187019_p3812176392"></a>8000</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0107187019_row9881783912"><td class="cellrowborder" valign="top" width="19.01190119011901%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0107187019_p158161773917"><a name="zh-cn_topic_0107187019_p158161773917"></a><a name="zh-cn_topic_0107187019_p158161773917"></a>数据库</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.8058805880588%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0107187019_p48111711396"><a name="zh-cn_topic_0107187019_p48111711396"></a><a name="zh-cn_topic_0107187019_p48111711396"></a>数据库名称。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.182218221822183%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0107187019_p98817133916"><a name="zh-cn_topic_0107187019_p98817133916"></a><a name="zh-cn_topic_0107187019_p98817133916"></a>postgres</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0107187019_row79151714394"><td class="cellrowborder" valign="top" width="19.01190119011901%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0107187019_p081117133920"><a name="zh-cn_topic_0107187019_p081117133920"></a><a name="zh-cn_topic_0107187019_p081117133920"></a>用户名</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.8058805880588%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0107187019_p10911171395"><a name="zh-cn_topic_0107187019_p10911171395"></a><a name="zh-cn_topic_0107187019_p10911171395"></a>所要连接数据库的用户名。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.182218221822183%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0107187019_p10991783915"><a name="zh-cn_topic_0107187019_p10991783915"></a><a name="zh-cn_topic_0107187019_p10991783915"></a>-</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0107187019_row18961717397"><td class="cellrowborder" valign="top" width="19.01190119011901%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0107187019_p1391917163910"><a name="zh-cn_topic_0107187019_p1391917163910"></a><a name="zh-cn_topic_0107187019_p1391917163910"></a>密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.8058805880588%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0107187019_p149101753912"><a name="zh-cn_topic_0107187019_p149101753912"></a><a name="zh-cn_topic_0107187019_p149101753912"></a>所要连接数据库的登录密码。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.182218221822183%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0107187019_p9921719399"><a name="zh-cn_topic_0107187019_p9921719399"></a><a name="zh-cn_topic_0107187019_p9921719399"></a>-</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0107187019_row86069127252"><td class="cellrowborder" valign="top" width="19.01190119011901%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0107187019_p3607121212519"><a name="zh-cn_topic_0107187019_p3607121212519"></a><a name="zh-cn_topic_0107187019_p3607121212519"></a>保存密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.8058805880588%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0107187019_p17607111212511"><a name="zh-cn_topic_0107187019_p17607111212511"></a><a name="zh-cn_topic_0107187019_p17607111212511"></a>在下拉列表中选择：</p>
    <a name="zh-cn_topic_0107187019_ul37500309263"></a><a name="zh-cn_topic_0107187019_ul37500309263"></a><ul id="zh-cn_topic_0107187019_ul37500309263"><li><strong id="zh-cn_topic_0107187019_b1675011302264"><a name="zh-cn_topic_0107187019_b1675011302264"></a><a name="zh-cn_topic_0107187019_b1675011302264"></a><span class="uicontrol" id="zh-cn_topic_0107187019_uicontrol1226118213278"><a name="zh-cn_topic_0107187019_uicontrol1226118213278"></a><a name="zh-cn_topic_0107187019_uicontrol1226118213278"></a>“仅当前会话”</span></strong>：仅在当前会话中保存密码。</li><li><strong id="zh-cn_topic_0107187019_b1091204022619"><a name="zh-cn_topic_0107187019_b1091204022619"></a><a name="zh-cn_topic_0107187019_b1091204022619"></a><span class="uicontrol" id="zh-cn_topic_0107187019_uicontrol72114622712"><a name="zh-cn_topic_0107187019_uicontrol72114622712"></a><a name="zh-cn_topic_0107187019_uicontrol72114622712"></a>“不保存”</span></strong>：不保存密码。</li></ul>
    </td>
    <td class="cellrowborder" valign="top" width="22.182218221822183%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0107187019_p5607512192513"><a name="zh-cn_topic_0107187019_p5607512192513"></a><a name="zh-cn_topic_0107187019_p5607512192513"></a>-</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0107187019_row1380819420192"><td class="cellrowborder" valign="top" width="19.01190119011901%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0107187019_p880824281913"><a name="zh-cn_topic_0107187019_p880824281913"></a><a name="zh-cn_topic_0107187019_p880824281913"></a>启用SSL</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.8058805880588%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0107187019_p1480994211197"><a name="zh-cn_topic_0107187019_p1480994211197"></a><a name="zh-cn_topic_0107187019_p1480994211197"></a>启用时，客户端将使用SSL加密连接方式。SSL连接方式安全性高于普通模式，建议开启。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.182218221822183%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0107187019_p280954217195"><a name="zh-cn_topic_0107187019_p280954217195"></a><a name="zh-cn_topic_0107187019_p280954217195"></a>-</p>
    </td>
    </tr>
    </tbody>
    </table>

    当“启用SSL”设置为开启时，请先参见[下载SSL证书](https://support.huaweicloud.com/mgtg-dws/dws_01_0083.html)下载SSL证书，并解压证书文件。然后，在如[图4](#zh-cn_topic_0107187019_fig27101723910)所示的窗口中单击“SSL“页签，设置如下参数：

    **表 2**  配置SSL参数

    <a name="zh-cn_topic_0107187019_table1512855203112"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0107187019_row171317551318"><th class="cellrowborder" valign="top" width="19.38%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0107187019_p18131955133117"><a name="zh-cn_topic_0107187019_p18131955133117"></a><a name="zh-cn_topic_0107187019_p18131955133117"></a>字段名称</p>
    </th>
    <th class="cellrowborder" valign="top" width="80.62%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0107187019_p19137554319"><a name="zh-cn_topic_0107187019_p19137554319"></a><a name="zh-cn_topic_0107187019_p19137554319"></a>说明</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0107187019_row61425513112"><td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0107187019_p1514955133113"><a name="zh-cn_topic_0107187019_p1514955133113"></a><a name="zh-cn_topic_0107187019_p1514955133113"></a>客户端SSL证书</p>
    </td>
    <td class="cellrowborder" valign="top" width="80.62%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0107187019_p3141055193115"><a name="zh-cn_topic_0107187019_p3141055193115"></a><a name="zh-cn_topic_0107187019_p3141055193115"></a>选择SSL证书解压目录下的<span class="filepath" id="zh-cn_topic_0107187019_filepath13178154343514"><a name="zh-cn_topic_0107187019_filepath13178154343514"></a><a name="zh-cn_topic_0107187019_filepath13178154343514"></a>“sslcert\client.crt”</span>文件。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0107187019_row15151555123117"><td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0107187019_p121516558317"><a name="zh-cn_topic_0107187019_p121516558317"></a><a name="zh-cn_topic_0107187019_p121516558317"></a>客户端SSL密钥</p>
    </td>
    <td class="cellrowborder" valign="top" width="80.62%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0107187019_p7151255113113"><a name="zh-cn_topic_0107187019_p7151255113113"></a><a name="zh-cn_topic_0107187019_p7151255113113"></a>从Data Studio 18.2.0 SPC1版本开始，客户端SSL秘钥只支持PK8格式。请选择SSL证书解压目录下的<span class="filepath" id="zh-cn_topic_0107187019_filepath780753173512"><a name="zh-cn_topic_0107187019_filepath780753173512"></a><a name="zh-cn_topic_0107187019_filepath780753173512"></a>“sslcert\client.key.pk8”</span>文件。</p>
    <p id="zh-cn_topic_0107187019_p8531535123613"><a name="zh-cn_topic_0107187019_p8531535123613"></a><a name="zh-cn_topic_0107187019_p8531535123613"></a>Data Studio 18.2.0 SPC1之前的版本，请选择SSL证书解压目录下的<span class="filepath" id="zh-cn_topic_0107187019_filepath53171556378"><a name="zh-cn_topic_0107187019_filepath53171556378"></a><a name="zh-cn_topic_0107187019_filepath53171556378"></a>“sslcert\client.key”</span>文件。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0107187019_row15151655103110"><td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0107187019_p91575583118"><a name="zh-cn_topic_0107187019_p91575583118"></a><a name="zh-cn_topic_0107187019_p91575583118"></a>根证书</p>
    </td>
    <td class="cellrowborder" valign="top" width="80.62%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0107187019_p1531243911409"><a name="zh-cn_topic_0107187019_p1531243911409"></a><a name="zh-cn_topic_0107187019_p1531243911409"></a>当<span class="parmname" id="zh-cn_topic_0107187019_parmname48081030144115"><a name="zh-cn_topic_0107187019_parmname48081030144115"></a><a name="zh-cn_topic_0107187019_parmname48081030144115"></a>“SSL模式”</span>设为<span class="parmvalue" id="zh-cn_topic_0107187019_parmvalue14808203011416"><a name="zh-cn_topic_0107187019_parmvalue14808203011416"></a><a name="zh-cn_topic_0107187019_parmvalue14808203011416"></a>“verify-ca”</span>时，必须设置根证书，请选择SSL证书解压目录下的<span class="filepath" id="zh-cn_topic_0107187019_filepath1754855718409"><a name="zh-cn_topic_0107187019_filepath1754855718409"></a><a name="zh-cn_topic_0107187019_filepath1754855718409"></a>“sslcert\cacert.pem”</span>文件。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0107187019_row51625510311"><td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0107187019_p516125517315"><a name="zh-cn_topic_0107187019_p516125517315"></a><a name="zh-cn_topic_0107187019_p516125517315"></a>SSL密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="80.62%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0107187019_p21655516313"><a name="zh-cn_topic_0107187019_p21655516313"></a><a name="zh-cn_topic_0107187019_p21655516313"></a>客户端pk8格式SSL秘钥密码，默认密码为<span class="parmvalue" id="zh-cn_topic_0107187019_parmvalue1742854019441"><a name="zh-cn_topic_0107187019_parmvalue1742854019441"></a><a name="zh-cn_topic_0107187019_parmvalue1742854019441"></a>“Gauss@MppDB”</span>。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0107187019_row1916155583118"><td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0107187019_p616115515312"><a name="zh-cn_topic_0107187019_p616115515312"></a><a name="zh-cn_topic_0107187019_p616115515312"></a>SSL模式</p>
    </td>
    <td class="cellrowborder" valign="top" width="80.62%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0107187019_p1380624518403"><a name="zh-cn_topic_0107187019_p1380624518403"></a><a name="zh-cn_topic_0107187019_p1380624518403"></a>GaussDB(DWS) 支持的SSL模式有：</p>
    <a name="zh-cn_topic_0107187019_ul174486715440"></a><a name="zh-cn_topic_0107187019_ul174486715440"></a><ul id="zh-cn_topic_0107187019_ul174486715440"><li>require</li><li>verify-ca</li></ul>
    <p id="zh-cn_topic_0107187019_p10351254114217"><a name="zh-cn_topic_0107187019_p10351254114217"></a><a name="zh-cn_topic_0107187019_p10351254114217"></a>GaussDB(DWS) 不支持<span class="parmvalue" id="zh-cn_topic_0107187019_parmvalue11879175512423"><a name="zh-cn_topic_0107187019_parmvalue11879175512423"></a><a name="zh-cn_topic_0107187019_parmvalue11879175512423"></a>“verify-full”</span>模式。</p>
    </td>
    </tr>
    </tbody>
    </table>

    **图 5**  配置SSL参数<a name="zh-cn_topic_0107187019_fig2491192219469"></a>  
    ![](figures/配置SSL参数.png "配置SSL参数")

9.  单击“确定“建立数据库连接。

    如果启用了SSL，在弹出的“连接安全告警“提示对话框中单击“继续“。

    登录成功后，将弹出“最近登录活动“提示框，表示Data Studio已经连接到数据库。用户即可在Data Studio界面的“SQL终端“窗口中执行SQL语句。

    **图 6**  登录成功<a name="zh-cn_topic_0107187019_fig1860617443213"></a>  
    ![](figures/登录成功.png "登录成功")

    欲详细了解Data Studio其他功能的使用方法，请按“F1“查看Data Studio用户手册。


