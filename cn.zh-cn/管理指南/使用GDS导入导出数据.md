# 使用GDS导入导出数据<a name="dws_01_0112_gds"></a>

当用户需要将远端服务器（例如，弹性云服务器）中的数据文件导入到DWS，或者将DWS数据库中的数据导出到远端服务器的数据文件中时，可以使用DWS提供的GDS导入导出数据的功能。

GDS（General Data Service）是DWS提供的数据并行加载工具。使用GDS导入数据到DWS，用户需要将GDS工具部署到数据源文件所在的服务器上，然后通过GDS外表设置的导入模式、导入数据格式等信息来识别数据源文件，利用DWS集群多节点并行的方式，将数据从数据源文件所在的服务器导入到DWS数据库中。数据源文件所在的服务器称为数据服务器，也称为GDS服务器。如果因数据量大，数据源文件存储在多个服务器上，则每个数据服务器上都需要安装配置、启动GDS。

使用GDS导出数据，则是将DWS中的数据以文件形式导出到部署了GDS工具的服务器上。

使用GDS导入或导出数据的流程如下：

1.  [准备GDS服务器](#section827248174616)
2.  [下载GDS工具包和SSL证书](#section690133817553)
3.  [使用GDS导入导出数据](#section2956857145514)

## 准备GDS服务器<a name="section827248174616"></a>

准备一个或多个主机，用于安装GDS工具包，作为GDS服务器。

作为GDS服务器的主机需满足以下要求：

-   GDS服务器的操作系统必须是GDS工具包所支持的操作系统，具体请参见[下载客户端](下载客户端.md)。
-   GDS服务器和DWS集群之间网络可以互通。
    -   DWS集群通过内网地址连接GDS服务器：

        -   需要创建一个弹性云服务器作为GDS服务器。
        -   创建的弹性云服务器与DWS集群应处于同一区域、同一虚拟私有云和子网。

        由于导入数据的速率会受网络带宽的影响，因此，推荐的方式是DWS集群通过内网地址连接GDS服务器。

    -   需要确保GDS服务器能够正常接收来自DWS集群的网络访问。

        端口：规划一个GDS服务的监听端口，该端口供DWS集群连接GDS服务器使用，用户在启动GDS服务时指定这个监听端口，如果不指定则默认端口为8098。

        防火墙：如果GDS服务器开启了防火墙，需要在防火墙中添加一个开放GDS服务监听端口的入方向的规则，以允许DWS集群通过该端口连接GDS服务器，否则将无法建立连接。

        >![](public_sys-resources/icon-note.gif) **说明：**   
        >注意，启动GDS服务时，监听端口请务必指定为这个已在防火墙中开放了的端口。  

        以创建一个弹性云服务器作为GDS服务器为例：

        首先，弹性云服务器所在的安全组需要添加入规则开放GDS服务的监听端口，示例如下：

        **表 1**  安全组入规则配置样例

        <a name="table84962718111"></a>
        <table><thead align="left"><tr id="row1950014781115"><th class="cellrowborder" valign="top" width="30.64%" id="mcps1.2.3.1.1"><p id="p1650012719114"><a name="p1650012719114"></a><a name="p1650012719114"></a><strong id="b155026761117"><a name="b155026761117"></a><a name="b155026761117"></a>参数名</strong></p>
        </th>
        <th class="cellrowborder" valign="top" width="69.36%" id="mcps1.2.3.1.2"><p id="p3502167101119"><a name="p3502167101119"></a><a name="p3502167101119"></a><strong id="b85041776117"><a name="b85041776117"></a><a name="b85041776117"></a>样例值</strong></p>
        </th>
        </tr>
        </thead>
        <tbody><tr id="row85051371114"><td class="cellrowborder" valign="top" width="30.64%" headers="mcps1.2.3.1.1 "><p id="p4507107131119"><a name="p4507107131119"></a><a name="p4507107131119"></a>协议</p>
        </td>
        <td class="cellrowborder" valign="top" width="69.36%" headers="mcps1.2.3.1.2 "><p id="p205088710117"><a name="p205088710117"></a><a name="p205088710117"></a>TCP</p>
        </td>
        </tr>
        <tr id="row125146716113"><td class="cellrowborder" valign="top" width="30.64%" headers="mcps1.2.3.1.1 "><p id="p1951611720118"><a name="p1951611720118"></a><a name="p1951611720118"></a>端口范围</p>
        </td>
        <td class="cellrowborder" valign="top" width="69.36%" headers="mcps1.2.3.1.2 "><p id="p25161577110"><a name="p25161577110"></a><a name="p25161577110"></a>5000</p>
        <div class="note" id="note1551616714118"><a name="note1551616714118"></a><a name="note1551616714118"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p145191873115"><a name="p145191873115"></a><a name="p145191873115"></a>此处需要输入GDS服务器的监听端口。</p>
        </div></div>
        </td>
        </tr>
        <tr id="row75194710119"><td class="cellrowborder" valign="top" width="30.64%" headers="mcps1.2.3.1.1 "><p id="p35209751112"><a name="p35209751112"></a><a name="p35209751112"></a>源地址</p>
        </td>
        <td class="cellrowborder" valign="top" width="69.36%" headers="mcps1.2.3.1.2 "><p id="p1552111711113"><a name="p1552111711113"></a><a name="p1552111711113"></a>选择“IP地址”，输入DWS集群地址，例如“192.168.0.10/32”。</p>
        </td>
        </tr>
        </tbody>
        </table>

        其次，弹性云服务器内部如果启用了防火墙，需要保证防火墙打开了GDS服务的监听端口：

        ```
        iptables  -I INPUT -p tcp -m tcp --dport <gds_port> -j ACCEPT
        ```



## 下载GDS工具包和SSL证书<a name="section690133817553"></a>

1.  通过访问以下地址登录DWS管理控制台：[https://console.huaweicloud.com/dws](https://console.huaweicloud.com/dws)。
2.  在左侧导航栏中，单击“连接管理“。
3.  在“gsql命令行客户端“的下拉列表中，选择对应版本的DWS客户端。客户端工具包中包含了GDS工具包和gsql客户端工具。

    请根据安装客户端的操作系统，选择“RedHat x64“或“SUSE x64“。

    -   “RedHat x64“客户端工具支持在以下系统中使用：
        -   RHEL6.4、6.5、6.6、6.7、7.1、7.2。
        -   CentOS6.4、6.5、6.6、6.7。
        -   EulerOS 2.0 SP2。

    -   “SUSE x64“客户端工具支持在以下系统中使用：

        SLES11 SP1/SP2/SP3/SP4。


4.  单击“下载“。
5.  （可选）如果要使用SSL加密方式启动GDS服务，请在“下载驱动程序“区域，单击“这里“下载SSL证书。

    使用SSL加密方式启动GDS服务，将对GDS服务器与DWS集群之间传输的数据进行加密，以保证数据的安全性。

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >SSL加密方式的安全性高于普通模式，建议采用SSL加密方式启动GDS服务。  


## 使用GDS导入导出数据<a name="section2956857145514"></a>

-   使用GDS导入数据到DWS集群

    详细操作请参见《数据仓库服务数据库开发指南》中的[使用GDS从远端服务器导入数据](https://support.huaweicloud.com/devg-dws/import_from_gds_0001.html)章节。

-   使用GDS从DWS集群导出数据

    详细操作请参见《数据仓库服务数据库开发指南》中的[使用GDS导出数据到远端服务器](https://support.huaweicloud.com/devg-dws/export_to_gds_0001.html)章节。


