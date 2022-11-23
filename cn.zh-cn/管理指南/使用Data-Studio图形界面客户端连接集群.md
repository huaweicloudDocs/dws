# 使用Data Studio图形界面客户端连接集群<a name="ZH-CN_TOPIC_0000001405317050"></a>

Data Studio是一款运行在Windows操作系统上的SQL客户端工具，有着丰富的GUI界面，能够管理数据库和数据库对象，编辑、运行、调试SQL脚本，查看执行计划等。在GaussDB\(DWS\) 管理控制台下载Data Studio软件包，解压后免安装即可使用。

DataStudio可供下载的版本分为“Windows x86“和“Windows x64“两种版本，分别支持32位和64位Windows操作系统。

## 连接集群前的准备<a name="section83156195500"></a>

-   已获取GaussDB\(DWS\) 集群的数据库管理员用户名和密码。
-   已获取GaussDB\(DWS\) 集群的公网访问地址，含IP地址和端口。具体请参见[获取集群连接地址](获取集群连接地址.md)。
-   已配置GaussDB\(DWS\) 集群所属的安全组，添加入规则允许用户的IP地址使用TCP访问端口。

    具体步骤，请参见《虚拟私有云用户指南》中的[添加安全组规则](https://support.huaweicloud.com/usermanual-vpc/zh-cn_topic_0030969470.html)章节。


## 使用Data Studio连接到集群数据库<a name="section12757151571018"></a>

1.  GaussDB\(DWS\) 提供了基于Windows平台的Data Studio图形界面客户端，该工具依赖JDK，请先在客户端主机上安装JDK。

    >![](public_sys-resources/icon-notice.gif) **须知：** 
    >仅支持Java 1.8版本的JDK。

    在Windows操作系统中，您可以访问[JDK官网](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)网站，下载符合操作系统版本的JDK，并根据指导进行安装。

2.  登录GaussDB\(DWS\) 管理控制台。
3.  单击“连接管理“。
4.  在“下载客户端和驱动“页面，下载“Data Studio图形界面客户端“。

    -   请根据操作系统类型，选择“Windows x86“或“Windows x64“，再单击“下载“，可以下载与现有集群版本匹配的Data Studio工具。

        如果同时拥有不同版本的集群，单击“下载”时会下载与集群最低版本相对应的Data Studio工具。如果当前没有集群，单击“下载”时将下载到低版本的Data Studio工具。GaussDB\(DWS\) 集群可向下兼容低版本的Data Studio工具。

    -   单击“历史版本”可根据集群版本下载相应版本的Data Studio工具，建议按集群版本下载配套的工具。

    **图 1**  下载客户端<a name="f61631d3c53004c5a82cea77f41476136"></a>  
    ![](figures/下载客户端.png "下载客户端")

    如果同时拥有不同版本的集群，系统会弹出对话框，提示您选择“集群版本“然后下载与集群版本相对应的客户端。在“集群管理“页面的集群列表中，单击指定集群的名称，再选择“集群详情“页签，可查看集群版本。

5.  解压下载的客户端软件包（32位或64位）到需要安装的路径。
6.  打开安装目录，双击Data Studio.exe，启动Data Studio客户端，如[图2](#febe974d888e24ddd8948572b362f7ef2)所示。

    **图 2**  启动客户端<a name="febe974d888e24ddd8948572b362f7ef2"></a>  
    ![](figures/启动客户端.png "启动客户端")

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >若您的电脑阻止应用运行，可对Data Studio.exe文件属性勾选解除锁定即可启动。

7.  在主菜单中选择 “文件\>新建连接” ，如[图3](#f5e30eb5f20c9434e971d8b2786b02dbf)所示。

    **图 3**  新建连接<a name="f5e30eb5f20c9434e971d8b2786b02dbf"></a>  
    ![](figures/新建连接.png "新建连接")

8.  在弹出的“新建/选择数据库连接“页面中，如下图所示，输入连接参数。

    **表 1**  配置连接参数

    <a name="t1af0ca815f7842d5a21fda355dc65bd1"></a>
    <table><thead align="left"><tr id="r998b3685340648cdafff9b1fe232c000"><th class="cellrowborder" valign="top" width="19.01190119011901%" id="mcps1.2.4.1.1"><p id="zh-cn_topic_0107187019_p167171710393"><a name="zh-cn_topic_0107187019_p167171710393"></a><a name="zh-cn_topic_0107187019_p167171710393"></a>字段名称</p>
    </th>
    <th class="cellrowborder" valign="top" width="58.8058805880588%" id="mcps1.2.4.1.2"><p id="zh-cn_topic_0107187019_p9741716392"><a name="zh-cn_topic_0107187019_p9741716392"></a><a name="zh-cn_topic_0107187019_p9741716392"></a>说明</p>
    </th>
    <th class="cellrowborder" valign="top" width="22.182218221822183%" id="mcps1.2.4.1.3"><p id="zh-cn_topic_0107187019_p88171713915"><a name="zh-cn_topic_0107187019_p88171713915"></a><a name="zh-cn_topic_0107187019_p88171713915"></a>举例</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="r666487d1871c4c67b803066814fc89a7"><td class="cellrowborder" valign="top" width="19.01190119011901%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0107187019_p51683131702"><a name="zh-cn_topic_0107187019_p51683131702"></a><a name="zh-cn_topic_0107187019_p51683131702"></a>数据库类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.8058805880588%" headers="mcps1.2.4.1.2 "><p id="p3297172210156"><a name="p3297172210156"></a><a name="p3297172210156"></a>选择“HUAWEI CLOUD DWS ”。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.182218221822183%" headers="mcps1.2.4.1.3 "><p id="p9374165110409"><a name="p9374165110409"></a><a name="p9374165110409"></a>HUAWEI CLOUD DWS</p>
    </td>
    </tr>
    <tr id="rd489ffeb99f8442387250de8fae31af8"><td class="cellrowborder" valign="top" width="19.01190119011901%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0107187019_p38131716399"><a name="zh-cn_topic_0107187019_p38131716399"></a><a name="zh-cn_topic_0107187019_p38131716399"></a>名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.8058805880588%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0107187019_p7813171399"><a name="zh-cn_topic_0107187019_p7813171399"></a><a name="zh-cn_topic_0107187019_p7813171399"></a>连接名称。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.182218221822183%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0107187019_p11813172392"><a name="zh-cn_topic_0107187019_p11813172392"></a><a name="zh-cn_topic_0107187019_p11813172392"></a>dws-demo</p>
    </td>
    </tr>
    <tr id="rb5e8545bc43e4b8a9a021ba41aeefe11"><td class="cellrowborder" valign="top" width="19.01190119011901%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0107187019_p12812176393"><a name="zh-cn_topic_0107187019_p12812176393"></a><a name="zh-cn_topic_0107187019_p12812176393"></a>主机</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.8058805880588%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0107187019_p38191720395"><a name="zh-cn_topic_0107187019_p38191720395"></a><a name="zh-cn_topic_0107187019_p38191720395"></a>所要连接的集群IP地址（IPv4）或域名。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.182218221822183%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0107187019_p88617143914"><a name="zh-cn_topic_0107187019_p88617143914"></a><a name="zh-cn_topic_0107187019_p88617143914"></a>-</p>
    </td>
    </tr>
    <tr id="r7afbb93b02494aedacc0d5cd192407a7"><td class="cellrowborder" valign="top" width="19.01190119011901%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0107187019_p88017123920"><a name="zh-cn_topic_0107187019_p88017123920"></a><a name="zh-cn_topic_0107187019_p88017123920"></a>端口号</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.8058805880588%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0107187019_p2861717396"><a name="zh-cn_topic_0107187019_p2861717396"></a><a name="zh-cn_topic_0107187019_p2861717396"></a>数据库端口。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.182218221822183%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0107187019_p3812176392"><a name="zh-cn_topic_0107187019_p3812176392"></a><a name="zh-cn_topic_0107187019_p3812176392"></a>8000</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0107187019_row9881783912"><td class="cellrowborder" valign="top" width="19.01190119011901%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0107187019_p158161773917"><a name="zh-cn_topic_0107187019_p158161773917"></a><a name="zh-cn_topic_0107187019_p158161773917"></a>数据库</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.8058805880588%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0107187019_p48111711396"><a name="zh-cn_topic_0107187019_p48111711396"></a><a name="zh-cn_topic_0107187019_p48111711396"></a>数据库名称。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.182218221822183%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0107187019_p98817133916"><a name="zh-cn_topic_0107187019_p98817133916"></a><a name="zh-cn_topic_0107187019_p98817133916"></a><span id="text5762101212489"><a name="text5762101212489"></a><a name="text5762101212489"></a>gaussdb</span></p>
    </td>
    </tr>
    <tr id="r616f149dd82b43129c47c6607bb17c91"><td class="cellrowborder" valign="top" width="19.01190119011901%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0107187019_p081117133920"><a name="zh-cn_topic_0107187019_p081117133920"></a><a name="zh-cn_topic_0107187019_p081117133920"></a>用户名</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.8058805880588%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0107187019_p10911171395"><a name="zh-cn_topic_0107187019_p10911171395"></a><a name="zh-cn_topic_0107187019_p10911171395"></a>所要连接数据库的用户名。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.182218221822183%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0107187019_p10991783915"><a name="zh-cn_topic_0107187019_p10991783915"></a><a name="zh-cn_topic_0107187019_p10991783915"></a>-</p>
    </td>
    </tr>
    <tr id="r61966e4859c54422b07d0a6601282b76"><td class="cellrowborder" valign="top" width="19.01190119011901%" headers="mcps1.2.4.1.1 "><p id="a43eee1cac6424178808d3748a272c2bb"><a name="a43eee1cac6424178808d3748a272c2bb"></a><a name="a43eee1cac6424178808d3748a272c2bb"></a>密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.8058805880588%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0107187019_p149101753912"><a name="zh-cn_topic_0107187019_p149101753912"></a><a name="zh-cn_topic_0107187019_p149101753912"></a>所要连接数据库的登录密码。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.182218221822183%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0107187019_p9921719399"><a name="zh-cn_topic_0107187019_p9921719399"></a><a name="zh-cn_topic_0107187019_p9921719399"></a>-</p>
    </td>
    </tr>
    <tr id="r9e3e4f337acc4f61b15fa1e0e998bcce"><td class="cellrowborder" valign="top" width="19.01190119011901%" headers="mcps1.2.4.1.1 "><p id="a28808cecbace4652988cbf02de8875cd"><a name="a28808cecbace4652988cbf02de8875cd"></a><a name="a28808cecbace4652988cbf02de8875cd"></a>保存密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.8058805880588%" headers="mcps1.2.4.1.2 "><p id="a2b9420d35de6421ea02d623eda4f67b1"><a name="a2b9420d35de6421ea02d623eda4f67b1"></a><a name="a2b9420d35de6421ea02d623eda4f67b1"></a>在下拉列表中选择：</p>
    <a name="zh-cn_topic_0107187019_ul37500309263"></a><a name="zh-cn_topic_0107187019_ul37500309263"></a><ul id="zh-cn_topic_0107187019_ul37500309263"><li><strong id="adb2e6088264e456ca8cddd167d3663a5"><a name="adb2e6088264e456ca8cddd167d3663a5"></a><a name="adb2e6088264e456ca8cddd167d3663a5"></a><span class="uicontrol" id="u42e2f00ff5c645779f736616302231b8"><a name="u42e2f00ff5c645779f736616302231b8"></a><a name="u42e2f00ff5c645779f736616302231b8"></a>“仅当前会话”</span></strong>：仅在当前会话中保存密码。</li><li><strong id="ac90e788518f64040948dace4fcd284ca"><a name="ac90e788518f64040948dace4fcd284ca"></a><a name="ac90e788518f64040948dace4fcd284ca"></a><span class="uicontrol" id="ub85a156dfc4a4f86bc6af49f533a2449"><a name="ub85a156dfc4a4f86bc6af49f533a2449"></a><a name="ub85a156dfc4a4f86bc6af49f533a2449"></a>“不保存”</span></strong>：不保存密码。</li></ul>
    </td>
    <td class="cellrowborder" valign="top" width="22.182218221822183%" headers="mcps1.2.4.1.3 "><p id="a84be3f8b1d4549e0adcf749640bc9dc0"><a name="a84be3f8b1d4549e0adcf749640bc9dc0"></a><a name="a84be3f8b1d4549e0adcf749640bc9dc0"></a>-</p>
    </td>
    </tr>
    <tr id="rb2cb4a7d7c254e898b8cf100733384c5"><td class="cellrowborder" valign="top" width="19.01190119011901%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0107187019_p880824281913"><a name="zh-cn_topic_0107187019_p880824281913"></a><a name="zh-cn_topic_0107187019_p880824281913"></a>启用SSL</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.8058805880588%" headers="mcps1.2.4.1.2 "><p id="a96a5bb2ce5dd4eddb9712b1ec340e207"><a name="a96a5bb2ce5dd4eddb9712b1ec340e207"></a><a name="a96a5bb2ce5dd4eddb9712b1ec340e207"></a>启用时，客户端将使用SSL加密连接方式。SSL连接方式安全性高于普通模式，建议开启。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.182218221822183%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0107187019_p280954217195"><a name="zh-cn_topic_0107187019_p280954217195"></a><a name="zh-cn_topic_0107187019_p280954217195"></a>-</p>
    </td>
    </tr>
    </tbody>
    </table>

    当“启用SSL”设置为开启时，请先参见[下载SSL证书](https://support.huaweicloud.com/mgtg-dws/dws_01_0038.html)下载SSL证书，并解压证书文件。然后单击“SSL“页签，设置如下参数：

    **表 2**  配置SSL参数

    <a name="tc6a4177683ae43a5a21e02a558b115d1"></a>
    <table><thead align="left"><tr id="re85a10ea61f04c57a14374ca5c7d6050"><th class="cellrowborder" valign="top" width="19.38%" id="mcps1.2.3.1.1"><p id="a033d348bbfd54eb4bbc8cfdcbe364f7c"><a name="a033d348bbfd54eb4bbc8cfdcbe364f7c"></a><a name="a033d348bbfd54eb4bbc8cfdcbe364f7c"></a>字段名称</p>
    </th>
    <th class="cellrowborder" valign="top" width="80.62%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0107187019_p19137554319"><a name="zh-cn_topic_0107187019_p19137554319"></a><a name="zh-cn_topic_0107187019_p19137554319"></a>说明</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="ra35932b78ca140b7a5439c9f7e3107ad"><td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.3.1.1 "><p id="a9ad6035d6045458ebf34506c32399247"><a name="a9ad6035d6045458ebf34506c32399247"></a><a name="a9ad6035d6045458ebf34506c32399247"></a>客户端SSL证书</p>
    </td>
    <td class="cellrowborder" valign="top" width="80.62%" headers="mcps1.2.3.1.2 "><p id="a8107c62bfd1d4ecfacf90307da3294d9"><a name="a8107c62bfd1d4ecfacf90307da3294d9"></a><a name="a8107c62bfd1d4ecfacf90307da3294d9"></a>选择SSL证书解压目录下的<span class="filepath" id="fea612bd9aaa44bd29b4bbc294e86e824"><a name="fea612bd9aaa44bd29b4bbc294e86e824"></a><a name="fea612bd9aaa44bd29b4bbc294e86e824"></a>“sslcert\client.crt”</span>文件。</p>
    </td>
    </tr>
    <tr id="r4a637f73e2164fa1bb65347c59e962cf"><td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0107187019_p121516558317"><a name="zh-cn_topic_0107187019_p121516558317"></a><a name="zh-cn_topic_0107187019_p121516558317"></a>客户端SSL密钥</p>
    </td>
    <td class="cellrowborder" valign="top" width="80.62%" headers="mcps1.2.3.1.2 "><p id="a5a76dbcc4fa74168be4ddd10f99571c7"><a name="a5a76dbcc4fa74168be4ddd10f99571c7"></a><a name="a5a76dbcc4fa74168be4ddd10f99571c7"></a>客户端SSL秘钥只支持PK8格式，请选择SSL证书解压目录下的<span class="filepath" id="fb583825ce4b140ea9367fcc975570233"><a name="fb583825ce4b140ea9367fcc975570233"></a><a name="fb583825ce4b140ea9367fcc975570233"></a>“sslcert\client.key.pk8”</span>文件。</p>
    </td>
    </tr>
    <tr id="re654cf33e6fd4162a322d30a10112453"><td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0107187019_p91575583118"><a name="zh-cn_topic_0107187019_p91575583118"></a><a name="zh-cn_topic_0107187019_p91575583118"></a>根证书</p>
    </td>
    <td class="cellrowborder" valign="top" width="80.62%" headers="mcps1.2.3.1.2 "><p id="ace66c1ada5ef40aba396d828d1cb5546"><a name="ace66c1ada5ef40aba396d828d1cb5546"></a><a name="ace66c1ada5ef40aba396d828d1cb5546"></a>当<span class="parmname" id="pe8f66a321c1d40eea2cfc295b2a991e8"><a name="pe8f66a321c1d40eea2cfc295b2a991e8"></a><a name="pe8f66a321c1d40eea2cfc295b2a991e8"></a>“SSL模式”</span>设为<span class="parmvalue" id="p48f1378b975a41769c3e51be4e2ba1f1"><a name="p48f1378b975a41769c3e51be4e2ba1f1"></a><a name="p48f1378b975a41769c3e51be4e2ba1f1"></a>“verify-ca”</span>时，必须设置根证书，请选择SSL证书解压目录下的<span class="filepath" id="fb1d54bb31b724c7eb09cc03e5cc54d29"><a name="fb1d54bb31b724c7eb09cc03e5cc54d29"></a><a name="fb1d54bb31b724c7eb09cc03e5cc54d29"></a>“sslcert\cacert.pem”</span>文件。</p>
    </td>
    </tr>
    <tr id="rc13e8815e6954b508b90480dd8dfc491"><td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0107187019_p516125517315"><a name="zh-cn_topic_0107187019_p516125517315"></a><a name="zh-cn_topic_0107187019_p516125517315"></a>SSL密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="80.62%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0107187019_p21655516313"><a name="zh-cn_topic_0107187019_p21655516313"></a><a name="zh-cn_topic_0107187019_p21655516313"></a>客户端pk8格式SSL秘钥密码。</p>
    </td>
    </tr>
    <tr id="r422d1cb572a34d88ae84caa91c68f153"><td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0107187019_p616115515312"><a name="zh-cn_topic_0107187019_p616115515312"></a><a name="zh-cn_topic_0107187019_p616115515312"></a>SSL模式</p>
    </td>
    <td class="cellrowborder" valign="top" width="80.62%" headers="mcps1.2.3.1.2 "><p id="aae9d413250a648b4b7f97d2aca66b196"><a name="aae9d413250a648b4b7f97d2aca66b196"></a><a name="aae9d413250a648b4b7f97d2aca66b196"></a>GaussDB(DWS) 支持的SSL模式有：</p>
    <a name="uef8cf175c60947de9f9cccfa40627114"></a><a name="uef8cf175c60947de9f9cccfa40627114"></a><ul id="uef8cf175c60947de9f9cccfa40627114"><li>require</li><li>verify-ca</li></ul>
    <p id="a294fdd7a18c04b48a350671d148ab611"><a name="a294fdd7a18c04b48a350671d148ab611"></a><a name="a294fdd7a18c04b48a350671d148ab611"></a>GaussDB(DWS) 不支持<span class="parmvalue" id="p0feb39a7d1394a7b8e5617054361eb9b"><a name="p0feb39a7d1394a7b8e5617054361eb9b"></a><a name="p0feb39a7d1394a7b8e5617054361eb9b"></a>“verify-full”</span>模式。</p>
    </td>
    </tr>
    </tbody>
    </table>

    **图 4**  配置SSL参数<a name="f5782e5489c5843a0be779dfbfbcd3a42"></a>  
    ![](figures/配置SSL参数.png "配置SSL参数")

9.  单击“确定“建立数据库连接。

    如果启用了SSL，在弹出的“连接安全告警“提示对话框中单击“继续“。

    登录成功后，将弹出“最近登录活动“提示框，表示Data Studio已经连接到数据库。用户即可在Data Studio界面的“SQL终端“窗口中执行SQL语句。

    **图 5**  登录成功<a name="fba153892b20741e79591551a71842471"></a>  
    ![](figures/登录成功.png "登录成功")

    欲详细了解Data Studio其他功能的使用方法，请按“F1“查看Data Studio用户手册。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >Data Studio中执行增删改查操作后不支持回滚数据。


