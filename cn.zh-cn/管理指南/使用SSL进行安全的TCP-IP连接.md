# 使用SSL进行安全的TCP/IP连接<a name="dws_01_0038"></a>

如果客户端或JDBC/ODBC应用程序要使用SSL连接方式，用户必须在客户端或应用程序代码中配置相关的SSL连接参数。DWS管理控制台提供了客户端所需的SSL证书，该SSL证书包含了客户端所需的默认证书、私钥、根证书以及私钥密码加密文件。请将该SSL证书下载到客户端所在的主机上，然后在客户端中指定证书所在的路径。

>![](public_sys-resources/icon-note.gif) **说明：** 
>使用默认的证书可能存在安全风险，为了提高系统安全性，强烈建议用户定期更换证书以避免被破解的风险。如果需要更换证书，请联系客服。

了解SSL证书的更多信息，请参见[（可选）下载SSL证书](（可选）下载SSL证书.md)。本章节主要介绍以下内容：

-   [在gsql客户端配置SSL认证相关的数字证书参数](#zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_s559f387461c440218ff2b33983a69004)
-   [SSL认证方式及客户端参数介绍](#zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_sf0c701b38d03417b8c969d148cd70223)

## 在gsql客户端配置SSL认证相关的数字证书参数<a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_s559f387461c440218ff2b33983a69004"></a>

DWS在集群部署完成后，默认已开启SSL认证模式。服务器端证书，私钥以及根证书已经默认配置完成。用户需要配置客户端的相关参数。

1.  登录DWS管理控制台，进入“连接管理”页面，下载SSL证书。

    关于SSL证书的更多信息，请参见[（可选）下载SSL证书](（可选）下载SSL证书.md)。

    **图 1**  SSL证书下载<a name="fig6639466014"></a>  
    ![](figures/SSL证书下载.png "SSL证书下载")

2.  使用文件传输工具（例如WinSCP工具）将SSL证书上传到客户端主机。

    例如，将下载的证书“dws\_ssl\_cert.tar.gz”存放到“/home/dbadmin/dws\_ssl/”目录下。

3.  使用SSH远程连接工具（例如PuTTY）登录gsql客户端主机，然后执行以下命令进入SSL证书的存放目录，并解压SSL证书：

    ```
    cd /home/dbadmin/dws_ssl/
    tar -xvf dws_ssl_cert.tar.gz
    ```

4.  在gsql客户端主机上，执行export命令，配置SSL认证相关的数字证书参数。

    SSL认证有两种认证方式：双向认证和单向认证，认证方式不同用户所需配置的客户端环境变量也不同，详细介绍请参见[SSL认证方式及客户端参数介绍](#zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_sf0c701b38d03417b8c969d148cd70223)。

    双向认证需配置如下参数：

    ```
    export PGSSLCERT="/home/dbadmin/dws_ssl/sslcert/client.crt"
    export PGSSLKEY="/home/dbadmin/dws_ssl/sslcert/client.key"
    export PGSSLMODE="verify-ca"
    export PGSSLROOTCERT="/home/dbadmin/dws_ssl/sslcert/cacert.pem"
    ```

    单向认证需要配置如下参数：

    ```
    export PGSSLMODE="verify-ca"
    export PGSSLROOTCERT="/home/dbadmin/dws_ssl/sslcert/cacert.pem"
    ```

    >![](public_sys-resources/icon-notice.gif) **须知：** 
    >-   从安全性考虑，建议使用双向认证方式。
    >-   配置客户端环境变量，必须包含文件的绝对路径。

5.  修改客户端密钥的权限。

    客户端根证书，密钥，证书以及密钥密码加密文件的权限，需保证权限为600。如果权限不满足要求，则客户端无法以SSL连接到集群。

    ```
    chmod 600 client.key
    chmod 600 client.crt
    chmod 600 client.key.cipher
    chmod 600 client.key.rand
    chmod 600 cacert.pem
    ```


## SSL认证方式及客户端参数介绍<a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_sf0c701b38d03417b8c969d148cd70223"></a>

SSL认证有两种认证方式，如[表1](#table267519441727)所示。从安全性考虑，建议使用双向认证方式。

**表 1**  认证方式

<a name="table267519441727"></a>
<table><thead align="left"><tr id="row1569712441123"><th class="cellrowborder" valign="top" width="11.991199119911991%" id="mcps1.2.5.1.1"><p id="p6706134413210"><a name="p6706134413210"></a><a name="p6706134413210"></a>认证方式</p>
</th>
<th class="cellrowborder" valign="top" width="29.24292429242924%" id="mcps1.2.5.1.2"><p id="p187063441212"><a name="p187063441212"></a><a name="p187063441212"></a>含义</p>
</th>
<th class="cellrowborder" valign="top" width="18.74187418741874%" id="mcps1.2.5.1.3"><p id="p17149441227"><a name="p17149441227"></a><a name="p17149441227"></a>配置客户端环境变量</p>
</th>
<th class="cellrowborder" valign="top" width="40.02400240024002%" id="mcps1.2.5.1.4"><p id="p371410441425"><a name="p371410441425"></a><a name="p371410441425"></a>维护建议</p>
</th>
</tr>
</thead>
<tbody><tr id="row167211244327"><td class="cellrowborder" valign="top" width="11.991199119911991%" headers="mcps1.2.5.1.1 "><p id="p20721184419215"><a name="p20721184419215"></a><a name="p20721184419215"></a>双向认证（推荐）</p>
</td>
<td class="cellrowborder" valign="top" width="29.24292429242924%" headers="mcps1.2.5.1.2 "><p id="p1772914441226"><a name="p1772914441226"></a><a name="p1772914441226"></a>客户端验证服务器证书的有效性，同时服务器端也要验证客户端证书的有效性，只有认证成功，连接才能建立。</p>
</td>
<td class="cellrowborder" valign="top" width="18.74187418741874%" headers="mcps1.2.5.1.3 "><p id="p872910441723"><a name="p872910441723"></a><a name="p872910441723"></a>设置如下环境变量：</p>
<a name="ul2072910443216"></a><a name="ul2072910443216"></a><ul id="ul2072910443216"><li>PGSSLCERT</li><li>PGSSLKEY</li><li>PGSSLROOTCERT</li><li>PGSSLMODE</li></ul>
</td>
<td class="cellrowborder" valign="top" width="40.02400240024002%" headers="mcps1.2.5.1.4 "><p id="p1575364414211"><a name="p1575364414211"></a><a name="p1575364414211"></a>该方式应用于安全性要求较高的场景。使用此方式时，建议设置客户端的PGSSLMODE变量为verify-ca。确保了网络数据的安全性。</p>
</td>
</tr>
<tr id="row1475394418216"><td class="cellrowborder" valign="top" width="11.991199119911991%" headers="mcps1.2.5.1.1 "><p id="p67533441527"><a name="p67533441527"></a><a name="p67533441527"></a>单向认证</p>
</td>
<td class="cellrowborder" valign="top" width="29.24292429242924%" headers="mcps1.2.5.1.2 "><p id="p27601449217"><a name="p27601449217"></a><a name="p27601449217"></a>客户端只验证服务器证书的有效性，而服务器端不验证客户端证书的有效性。服务器加载证书信息并发送给客户端，客户端使用根证书来验证服务器端证书的有效性。</p>
</td>
<td class="cellrowborder" valign="top" width="18.74187418741874%" headers="mcps1.2.5.1.3 "><p id="p976014441621"><a name="p976014441621"></a><a name="p976014441621"></a>设置如下环境变量：</p>
<a name="ul117605446218"></a><a name="ul117605446218"></a><ul id="ul117605446218"><li>PGSSLROOTCERT</li><li>PGSSLMODE</li></ul>
</td>
<td class="cellrowborder" valign="top" width="40.02400240024002%" headers="mcps1.2.5.1.4 "><p id="p8776154411212"><a name="p8776154411212"></a><a name="p8776154411212"></a>为防止基于TCP链接的欺骗，建议使用SSL证书认证功能。除配置客户端根证书外，建议客户端使用PGSSLMODE变量为verify-ca方式连接。</p>
</td>
</tr>
</tbody>
</table>

在客户端配置SSL认证相关的环境变量，详细信息请参见[表2](#zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_t1a20720af5504dc0ba3c5d0e8d1a028b)。

>![](public_sys-resources/icon-note.gif) **说明：** 
>客户端环境变量的路径以“_/home/dbadmin_/dws\_ssl/”为例，在实际操作中请使用实际路径进行替换。

**表 2**  客户端参数

<a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_t1a20720af5504dc0ba3c5d0e8d1a028b"></a>
<table><thead align="left"><tr id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_r075c7db3e29149b7935bd87da7c3f5e9"><th class="cellrowborder" valign="top" width="13.059999999999999%" id="mcps1.2.4.1.1"><p id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_aced8d9e6a1e9424c9f486cd2565a5f6b"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_aced8d9e6a1e9424c9f486cd2565a5f6b"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_aced8d9e6a1e9424c9f486cd2565a5f6b"></a>环境变量</p>
</th>
<th class="cellrowborder" valign="top" width="30.5%" id="mcps1.2.4.1.2"><p id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_af8aafa1cb5c2435b891d157ce1358aa3"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_af8aafa1cb5c2435b891d157ce1358aa3"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_af8aafa1cb5c2435b891d157ce1358aa3"></a>描述</p>
</th>
<th class="cellrowborder" valign="top" width="56.44%" id="mcps1.2.4.1.3"><p id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_af868a291814e47088c551bf14923e305"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_af868a291814e47088c551bf14923e305"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_af868a291814e47088c551bf14923e305"></a>取值范围</p>
</th>
</tr>
</thead>
<tbody><tr id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_r63de0425aa9e48648eddee2052c34099"><td class="cellrowborder" valign="top" width="13.059999999999999%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a79f122f5e8864d49958a01e2599232e2"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a79f122f5e8864d49958a01e2599232e2"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a79f122f5e8864d49958a01e2599232e2"></a>PGSSLCERT</p>
</td>
<td class="cellrowborder" valign="top" width="30.5%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a849a7114de984baa835520125891cc4c"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a849a7114de984baa835520125891cc4c"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a849a7114de984baa835520125891cc4c"></a>指定客户端证书文件，包含客户端的公钥。客户端证书用以表明客户端身份的合法性，公钥将发送给对端用来对数据进行加密。</p>
</td>
<td class="cellrowborder" valign="top" width="56.44%" headers="mcps1.2.4.1.3 "><div class="p" id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_aab9afb2d4ccb486584dc34925557eb5b"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_aab9afb2d4ccb486584dc34925557eb5b"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_aab9afb2d4ccb486584dc34925557eb5b"></a>必须包含文件的绝对路径，如：<pre class="screen" id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_sd1ee55d896da429d8a382c764a33570f"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_sd1ee55d896da429d8a382c764a33570f"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_sd1ee55d896da429d8a382c764a33570f"></a>export PGSSLCERT='<em id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a175d9cc2e30e4403a0f6963f5320c59d"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a175d9cc2e30e4403a0f6963f5320c59d"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a175d9cc2e30e4403a0f6963f5320c59d"></a>/home/dbadmin/dws_ssl/sslcert/client.crt</em>'</pre>
</div>
<p id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a659d086b20fd47b4998a10ba22739753"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a659d086b20fd47b4998a10ba22739753"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a659d086b20fd47b4998a10ba22739753"></a><strong id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_ab05988be024e4d0ab963f40a2ce47abe"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_ab05988be024e4d0ab963f40a2ce47abe"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_ab05988be024e4d0ab963f40a2ce47abe"></a>默认值</strong>：空</p>
</td>
</tr>
<tr id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_r9b2094fa73ea44a7bf3381223937f92d"><td class="cellrowborder" valign="top" width="13.059999999999999%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a2c015bd8e62a452ab7e647e7d56e65bf"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a2c015bd8e62a452ab7e647e7d56e65bf"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a2c015bd8e62a452ab7e647e7d56e65bf"></a>PGSSLKEY</p>
</td>
<td class="cellrowborder" valign="top" width="30.5%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_aaa8e11b80a95489c8a5ab1d3df31ca1a"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_aaa8e11b80a95489c8a5ab1d3df31ca1a"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_aaa8e11b80a95489c8a5ab1d3df31ca1a"></a>指定客户端私钥文件，用以数字签名和对公钥加密的数据进行解密。</p>
</td>
<td class="cellrowborder" valign="top" width="56.44%" headers="mcps1.2.4.1.3 "><div class="p" id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a953393a0d05f4b8a8a379fc52554c838"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a953393a0d05f4b8a8a379fc52554c838"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a953393a0d05f4b8a8a379fc52554c838"></a>必须包含文件的绝对路径，如：<pre class="screen" id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_s65d035eba41841268050e954fe6c267d"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_s65d035eba41841268050e954fe6c267d"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_s65d035eba41841268050e954fe6c267d"></a>export PGSSLKEY='<em id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_zh-cn_topic_0058967691_i162643549168"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_zh-cn_topic_0058967691_i162643549168"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_zh-cn_topic_0058967691_i162643549168"></a>/home/dbadmin/dws_ssl/sslcert/client.key</em>'</pre>
</div>
<p id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_ab15b4d40daf04a32b1d42d1defd838ba"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_ab15b4d40daf04a32b1d42d1defd838ba"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_ab15b4d40daf04a32b1d42d1defd838ba"></a><strong id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_ab803f48b32da47b583c01a6447e4b868"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_ab803f48b32da47b583c01a6447e4b868"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_ab803f48b32da47b583c01a6447e4b868"></a>默认值</strong>：空</p>
</td>
</tr>
<tr id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_rb472cd1e8b42453f9a0b255b07416f14"><td class="cellrowborder" valign="top" width="13.059999999999999%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a54a9c62cc83c4c749125c3d9bad6e67e"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a54a9c62cc83c4c749125c3d9bad6e67e"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a54a9c62cc83c4c749125c3d9bad6e67e"></a>PGSSLMODE</p>
</td>
<td class="cellrowborder" valign="top" width="30.5%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a0c97d7d4943249a79adec5801937ecb7"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a0c97d7d4943249a79adec5801937ecb7"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a0c97d7d4943249a79adec5801937ecb7"></a>设置是否和服务器进行SSL连接协商，以及指定SSL连接的优先级。</p>
</td>
<td class="cellrowborder" valign="top" width="56.44%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_aee9d6bd66fde45c2bfa2efab0cf85cee"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_aee9d6bd66fde45c2bfa2efab0cf85cee"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_aee9d6bd66fde45c2bfa2efab0cf85cee"></a><strong id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a10d47a31a1c542e2afa4193adcbf332b"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a10d47a31a1c542e2afa4193adcbf332b"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a10d47a31a1c542e2afa4193adcbf332b"></a>取值及含义：</strong></p>
<a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_u5a3aa83f2351407caf0185281284d463"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_u5a3aa83f2351407caf0185281284d463"></a><ul id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_u5a3aa83f2351407caf0185281284d463"><li>disable：只尝试非SSL连接。</li><li>allow：首先尝试非SSL连接，如果连接失败，再尝试SSL连接。</li><li>prefer：首先尝试SSL连接，如果连接失败，将尝试非SSL连接。</li><li>require：只尝试SSL连接。如果存在CA文件，则按设置成verify-ca的方式验证。</li><li>verify-ca：只尝试SSL连接，并且验证服务器是否具有由可信任的证书机构签发的证书。</li><li>verify-full：DWS不支持此模式。</li></ul>
<p id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_ad3fef165034244089c01c2d643a6ffdf"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_ad3fef165034244089c01c2d643a6ffdf"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_ad3fef165034244089c01c2d643a6ffdf"></a><strong id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a2364f46f3816402a8672d4288826bda0"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a2364f46f3816402a8672d4288826bda0"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a2364f46f3816402a8672d4288826bda0"></a>默认值：</strong>prefer</p>
</td>
</tr>
<tr id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_reab62f605d8b423f9ad0ce2714fe76e6"><td class="cellrowborder" valign="top" width="13.059999999999999%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a366d8b9fdb914a8b8e179afb9424bc5b"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a366d8b9fdb914a8b8e179afb9424bc5b"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a366d8b9fdb914a8b8e179afb9424bc5b"></a>PGSSLROOTCERT</p>
</td>
<td class="cellrowborder" valign="top" width="30.5%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a32096b73c9114ef99b7d88064548fffa"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a32096b73c9114ef99b7d88064548fffa"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a32096b73c9114ef99b7d88064548fffa"></a>指定为客户端颁发证书的根证书文件，根证书用于验证服务器证书的有效性。</p>
</td>
<td class="cellrowborder" valign="top" width="56.44%" headers="mcps1.2.4.1.3 "><div class="p" id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a46db14e6a0f444368d713c0a3f5b03ee"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a46db14e6a0f444368d713c0a3f5b03ee"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a46db14e6a0f444368d713c0a3f5b03ee"></a>必须包含文件的绝对路径，如：<pre class="screen" id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_s2d94e458c7ab47a2aaaa15d97ffcc658"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_s2d94e458c7ab47a2aaaa15d97ffcc658"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_s2d94e458c7ab47a2aaaa15d97ffcc658"></a>export PGSSLROOTCERT='<em id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_af1aa145e4168496ca7de9d4182ac6b29"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_af1aa145e4168496ca7de9d4182ac6b29"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_af1aa145e4168496ca7de9d4182ac6b29"></a>/home<em id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_zh-cn_topic_0058967691_i253753991625"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_zh-cn_topic_0058967691_i253753991625"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_zh-cn_topic_0058967691_i253753991625"></a>/dbadmin</em>/dws_ssl/sslcert/certca.pem</em>'</pre>
</div>
<p id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a271adf4f3e1848a3ae44f427f6fb983d"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a271adf4f3e1848a3ae44f427f6fb983d"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a271adf4f3e1848a3ae44f427f6fb983d"></a><strong id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_ac89c69c0244e488d8eab5cddbb6b0269"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_ac89c69c0244e488d8eab5cddbb6b0269"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_ac89c69c0244e488d8eab5cddbb6b0269"></a>默认值：</strong>空</p>
</td>
</tr>
<tr id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_r90ba7e36f5e447c29a5e6941da52c130"><td class="cellrowborder" valign="top" width="13.059999999999999%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_aeb330e5acd614a59b7ea7742987fd0de"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_aeb330e5acd614a59b7ea7742987fd0de"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_aeb330e5acd614a59b7ea7742987fd0de"></a>PGSSLCRL</p>
</td>
<td class="cellrowborder" valign="top" width="30.5%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a0d9a328c7578483497420c431d0fd818"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a0d9a328c7578483497420c431d0fd818"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a0d9a328c7578483497420c431d0fd818"></a>指定证书吊销列表文件，用于验证服务器证书是否在废弃证书列表中，如果在，则服务器证书将会被视为无效证书。</p>
</td>
<td class="cellrowborder" valign="top" width="56.44%" headers="mcps1.2.4.1.3 "><div class="p" id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_abcf7b6ca0d9a47b7a15dae7cc7ce39ad"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_abcf7b6ca0d9a47b7a15dae7cc7ce39ad"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_abcf7b6ca0d9a47b7a15dae7cc7ce39ad"></a>必须包含文件的绝对路径，如：<pre class="screen" id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_s819dac6238bb40ff947c71e379e48246"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_s819dac6238bb40ff947c71e379e48246"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_s819dac6238bb40ff947c71e379e48246"></a>export PGSSLCRL='<em id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_ac29e84d07c1f46e4a56b7b8500c6f1f0"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_ac29e84d07c1f46e4a56b7b8500c6f1f0"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_ac29e84d07c1f46e4a56b7b8500c6f1f0"></a>/home/dbadmin/dws_ssl/sslcert/sslcrl-file.crl</em>'</pre>
</div>
<p id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a5f56fdaa783e4a1986a457f445969fe2"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a5f56fdaa783e4a1986a457f445969fe2"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_a5f56fdaa783e4a1986a457f445969fe2"></a><strong id="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_af6ecb350e9244540a7d7fe8ad620ee90"><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_af6ecb350e9244540a7d7fe8ad620ee90"></a><a name="zh-cn_topic_0111534129_zh-cn_topic_0110494598_zh-cn_topic_0110355482_zh-cn_topic_0085031978_zh-cn_topic_0059778374_af6ecb350e9244540a7d7fe8ad620ee90"></a>默认值：</strong>空</p>
</td>
</tr>
</tbody>
</table>

