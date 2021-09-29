# 使用SSL进行安全的TCP/IP连接<a name="ZH-CN_TOPIC_0000001145696569"></a>

如果客户端或JDBC/ODBC应用程序要使用SSL连接方式，用户必须在客户端或应用程序代码中配置相关的SSL连接参数。GaussDB\(DWS\) 管理控制台提供了客户端所需的SSL证书，该SSL证书包含了客户端所需的默认证书、私钥、根证书以及私钥密码加密文件。请将该SSL证书下载到客户端所在的主机上，然后在客户端中指定证书所在的路径。

>![](public_sys-resources/icon-note.gif) **说明：** 
>使用默认的证书可能存在安全风险，为了提高系统安全性，强烈建议用户定期更换证书以避免被破解的风险。如果需要更换证书，请联系客服。

了解SSL证书的更多信息，请参见[（可选）下载SSL证书](（可选）下载SSL证书.md)。本章节主要介绍以下内容：

-   [在gsql客户端配置SSL认证相关的数字证书参数](#s6d3b0bb119894929810147678d9c67a5)
-   [SSL认证方式及客户端参数介绍](#s3a228fb4ac9c48ec8bc34e812c8879e8)

## 在gsql客户端配置SSL认证相关的数字证书参数<a name="s6d3b0bb119894929810147678d9c67a5"></a>

GaussDB\(DWS\) 在集群部署完成后，默认已开启SSL认证模式。服务器端证书，私钥以及根证书已经默认配置完成。用户需要配置客户端的相关参数。

1.  登录GaussDB\(DWS\) 管理控制台，进入“连接管理”页面，下载SSL证书。

    关于SSL证书的更多信息，请参见[（可选）下载SSL证书](（可选）下载SSL证书.md)。

    **图 1**  SSL证书下载<a name="fig6639466014"></a>  
    ![](figures/SSL证书下载.png "SSL证书下载")

2.  使用文件传输工具（例如WinSCP工具）将SSL证书上传到客户端主机。

    例如，将下载的证书“dws\_ssl\_cert.zip”存放到“/home/dbadmin/dws\_ssl/”目录下。

3.  使用SSH远程连接工具（例如PuTTY）登录gsql客户端主机，然后执行以下命令进入SSL证书的存放目录，并解压SSL证书：

    ```
    cd /home/dbadmin/dws_ssl/
    unzip dws_ssl_cert.zip
    ```

4.  在gsql客户端主机上，执行export命令，配置SSL认证相关的数字证书参数。

    SSL认证有两种认证方式：双向认证和单向认证，认证方式不同用户所需配置的客户端环境变量也不同，详细介绍请参见[SSL认证方式及客户端参数介绍](#s3a228fb4ac9c48ec8bc34e812c8879e8)。

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


## SSL认证方式及客户端参数介绍<a name="s3a228fb4ac9c48ec8bc34e812c8879e8"></a>

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

在客户端配置SSL认证相关的环境变量，详细信息请参见[表2](#t8b0644779e4c40009b6fb1ad6a8ea986)。

>![](public_sys-resources/icon-note.gif) **说明：** 
>客户端环境变量的路径以“_/home/dbadmin_/dws\_ssl/”为例，在实际操作中请使用实际路径进行替换。

**表 2**  客户端参数

<a name="t8b0644779e4c40009b6fb1ad6a8ea986"></a>
<table><thead align="left"><tr id="r43822a39dba648828fe49912078f1cb2"><th class="cellrowborder" valign="top" width="13.059999999999999%" id="mcps1.2.4.1.1"><p id="ad17d7af1c3de4d729bf57312c91e6974"><a name="ad17d7af1c3de4d729bf57312c91e6974"></a><a name="ad17d7af1c3de4d729bf57312c91e6974"></a>环境变量</p>
</th>
<th class="cellrowborder" valign="top" width="30.5%" id="mcps1.2.4.1.2"><p id="ac380e0ec1bd34540bfbfd4e6cb96972f"><a name="ac380e0ec1bd34540bfbfd4e6cb96972f"></a><a name="ac380e0ec1bd34540bfbfd4e6cb96972f"></a>描述</p>
</th>
<th class="cellrowborder" valign="top" width="56.44%" id="mcps1.2.4.1.3"><p id="ac9474bec612d44f08a364a81701c28a1"><a name="ac9474bec612d44f08a364a81701c28a1"></a><a name="ac9474bec612d44f08a364a81701c28a1"></a>取值范围</p>
</th>
</tr>
</thead>
<tbody><tr id="r972797e6e649495cac959b5ec60d1dca"><td class="cellrowborder" valign="top" width="13.059999999999999%" headers="mcps1.2.4.1.1 "><p id="ae1ed5b266db84f2d9556f32663a3be24"><a name="ae1ed5b266db84f2d9556f32663a3be24"></a><a name="ae1ed5b266db84f2d9556f32663a3be24"></a>PGSSLCERT</p>
</td>
<td class="cellrowborder" valign="top" width="30.5%" headers="mcps1.2.4.1.2 "><p id="a01cc006c5316402e8f6a4a9296d2c8bf"><a name="a01cc006c5316402e8f6a4a9296d2c8bf"></a><a name="a01cc006c5316402e8f6a4a9296d2c8bf"></a>指定客户端证书文件，包含客户端的公钥。客户端证书用以表明客户端身份的合法性，公钥将发送给对端用来对数据进行加密。</p>
</td>
<td class="cellrowborder" valign="top" width="56.44%" headers="mcps1.2.4.1.3 "><div class="p" id="a156de78bab614d698e120a40cc086b45"><a name="a156de78bab614d698e120a40cc086b45"></a><a name="a156de78bab614d698e120a40cc086b45"></a>必须包含文件的绝对路径，如：<pre class="screen" id="s24de87000fcf43b0b5531d835b2dae56"><a name="s24de87000fcf43b0b5531d835b2dae56"></a><a name="s24de87000fcf43b0b5531d835b2dae56"></a>export PGSSLCERT='<em id="a2d5b5f13eb5b43aeb17f6a00d3a858d2"><a name="a2d5b5f13eb5b43aeb17f6a00d3a858d2"></a><a name="a2d5b5f13eb5b43aeb17f6a00d3a858d2"></a>/home/dbadmin/dws_ssl/sslcert/client.crt</em>'</pre>
</div>
<p id="acdf675a9057d403c917bc1dcc49806c2"><a name="acdf675a9057d403c917bc1dcc49806c2"></a><a name="acdf675a9057d403c917bc1dcc49806c2"></a><strong id="adb8d89b5174145f597004b424d407c5b"><a name="adb8d89b5174145f597004b424d407c5b"></a><a name="adb8d89b5174145f597004b424d407c5b"></a>默认值</strong>：空</p>
</td>
</tr>
<tr id="rc98ff95b80ef4f88bc66c12fe5410d32"><td class="cellrowborder" valign="top" width="13.059999999999999%" headers="mcps1.2.4.1.1 "><p id="a51893fa2bd9b4568a84f40fb815973aa"><a name="a51893fa2bd9b4568a84f40fb815973aa"></a><a name="a51893fa2bd9b4568a84f40fb815973aa"></a>PGSSLKEY</p>
</td>
<td class="cellrowborder" valign="top" width="30.5%" headers="mcps1.2.4.1.2 "><p id="a9de3b54755c444c1b6c0ae8431197b62"><a name="a9de3b54755c444c1b6c0ae8431197b62"></a><a name="a9de3b54755c444c1b6c0ae8431197b62"></a>指定客户端私钥文件，用以数字签名和对公钥加密的数据进行解密。</p>
</td>
<td class="cellrowborder" valign="top" width="56.44%" headers="mcps1.2.4.1.3 "><div class="p" id="a8da9a9daae1a4ece8be3ad6b44637ec5"><a name="a8da9a9daae1a4ece8be3ad6b44637ec5"></a><a name="a8da9a9daae1a4ece8be3ad6b44637ec5"></a>必须包含文件的绝对路径，如：<pre class="screen" id="sc413cfb21de442cd9a16f1129e591f3b"><a name="sc413cfb21de442cd9a16f1129e591f3b"></a><a name="sc413cfb21de442cd9a16f1129e591f3b"></a>export PGSSLKEY='<em id="aca6668f8e3bb4b87857021cded5fad09"><a name="aca6668f8e3bb4b87857021cded5fad09"></a><a name="aca6668f8e3bb4b87857021cded5fad09"></a>/home/dbadmin/dws_ssl/sslcert/client.key</em>'</pre>
</div>
<p id="a39ee87ea493d4270b5f44b92d991148d"><a name="a39ee87ea493d4270b5f44b92d991148d"></a><a name="a39ee87ea493d4270b5f44b92d991148d"></a><strong id="a5313240e7ed54529a3b7367949a153ab"><a name="a5313240e7ed54529a3b7367949a153ab"></a><a name="a5313240e7ed54529a3b7367949a153ab"></a>默认值</strong>：空</p>
</td>
</tr>
<tr id="r85fe97858f3943ecae36f9597d96a226"><td class="cellrowborder" valign="top" width="13.059999999999999%" headers="mcps1.2.4.1.1 "><p id="a28fb67e3d7874c55a98063af0ad3f8ef"><a name="a28fb67e3d7874c55a98063af0ad3f8ef"></a><a name="a28fb67e3d7874c55a98063af0ad3f8ef"></a>PGSSLMODE</p>
</td>
<td class="cellrowborder" valign="top" width="30.5%" headers="mcps1.2.4.1.2 "><p id="abee299539baa4dfcbbdced408c233f87"><a name="abee299539baa4dfcbbdced408c233f87"></a><a name="abee299539baa4dfcbbdced408c233f87"></a>设置是否和服务器进行SSL连接协商，以及指定SSL连接的优先级。</p>
</td>
<td class="cellrowborder" valign="top" width="56.44%" headers="mcps1.2.4.1.3 "><p id="a5d279ea1261e4998a2d42805bf535ad3"><a name="a5d279ea1261e4998a2d42805bf535ad3"></a><a name="a5d279ea1261e4998a2d42805bf535ad3"></a><strong id="ab9953869fbfd4250aecb5dfc7aee682d"><a name="ab9953869fbfd4250aecb5dfc7aee682d"></a><a name="ab9953869fbfd4250aecb5dfc7aee682d"></a>取值及含义：</strong></p>
<a name="u48e2dabb7bdc47eea753bf8035b63f2a"></a><a name="u48e2dabb7bdc47eea753bf8035b63f2a"></a><ul id="u48e2dabb7bdc47eea753bf8035b63f2a"><li>disable：只尝试非SSL连接。</li><li>allow：首先尝试非SSL连接，如果连接失败，再尝试SSL连接。</li><li>prefer：首先尝试SSL连接，如果连接失败，将尝试非SSL连接。</li><li>require：只尝试SSL连接。如果存在CA文件，则按设置成verify-ca的方式验证。</li><li>verify-ca：只尝试SSL连接，并且验证服务器是否具有由可信任的证书机构签发的证书。</li><li>verify-full：GaussDB(DWS) 不支持此模式。</li></ul>
<p id="aa440c62ceb0e49b396c7289c5149fd58"><a name="aa440c62ceb0e49b396c7289c5149fd58"></a><a name="aa440c62ceb0e49b396c7289c5149fd58"></a><strong id="a46cf326b8e1a4eeaa03f1dba7cd5d5f1"><a name="a46cf326b8e1a4eeaa03f1dba7cd5d5f1"></a><a name="a46cf326b8e1a4eeaa03f1dba7cd5d5f1"></a>默认值：</strong>prefer</p>
</td>
</tr>
<tr id="r705a9febfc4e4eca8059bc5b91dc733f"><td class="cellrowborder" valign="top" width="13.059999999999999%" headers="mcps1.2.4.1.1 "><p id="a86405aec64294a4c8feaf5fa7155363d"><a name="a86405aec64294a4c8feaf5fa7155363d"></a><a name="a86405aec64294a4c8feaf5fa7155363d"></a>PGSSLROOTCERT</p>
</td>
<td class="cellrowborder" valign="top" width="30.5%" headers="mcps1.2.4.1.2 "><p id="a6a09560a39d14ed8b4755dce027303d3"><a name="a6a09560a39d14ed8b4755dce027303d3"></a><a name="a6a09560a39d14ed8b4755dce027303d3"></a>指定为客户端颁发证书的根证书文件，根证书用于验证服务器证书的有效性。</p>
</td>
<td class="cellrowborder" valign="top" width="56.44%" headers="mcps1.2.4.1.3 "><div class="p" id="a8bffd67e95b24511b2c9c6ba23949e26"><a name="a8bffd67e95b24511b2c9c6ba23949e26"></a><a name="a8bffd67e95b24511b2c9c6ba23949e26"></a>必须包含文件的绝对路径，如：<pre class="screen" id="s52013b02b46c4f7dac1fcadc8e5caa0e"><a name="s52013b02b46c4f7dac1fcadc8e5caa0e"></a><a name="s52013b02b46c4f7dac1fcadc8e5caa0e"></a>export PGSSLROOTCERT='<em id="a6a6171cbc744465188da02c71fa55f68"><a name="a6a6171cbc744465188da02c71fa55f68"></a><a name="a6a6171cbc744465188da02c71fa55f68"></a>/home<em id="a2658be24cedf49d789f052315ae826e7"><a name="a2658be24cedf49d789f052315ae826e7"></a><a name="a2658be24cedf49d789f052315ae826e7"></a>/dbadmin</em>/dws_ssl/sslcert/certca.pem</em>'</pre>
</div>
<p id="a19a2340265474308a47f45edbba76799"><a name="a19a2340265474308a47f45edbba76799"></a><a name="a19a2340265474308a47f45edbba76799"></a><strong id="aa6b88800f677424cab9faa2016bf7a68"><a name="aa6b88800f677424cab9faa2016bf7a68"></a><a name="aa6b88800f677424cab9faa2016bf7a68"></a>默认值：</strong>空</p>
</td>
</tr>
<tr id="r8204337653ba459d96d1ed621f76bf9a"><td class="cellrowborder" valign="top" width="13.059999999999999%" headers="mcps1.2.4.1.1 "><p id="a77efe9c8ef7c4214accae3549749a432"><a name="a77efe9c8ef7c4214accae3549749a432"></a><a name="a77efe9c8ef7c4214accae3549749a432"></a>PGSSLCRL</p>
</td>
<td class="cellrowborder" valign="top" width="30.5%" headers="mcps1.2.4.1.2 "><p id="a502b2159a2984570942c2b09a82420a9"><a name="a502b2159a2984570942c2b09a82420a9"></a><a name="a502b2159a2984570942c2b09a82420a9"></a>指定证书吊销列表文件，用于验证服务器证书是否在废弃证书列表中，如果在，则服务器证书将会被视为无效证书。</p>
</td>
<td class="cellrowborder" valign="top" width="56.44%" headers="mcps1.2.4.1.3 "><div class="p" id="a09da1ca77fee42e6b12a1fcb99a1bd79"><a name="a09da1ca77fee42e6b12a1fcb99a1bd79"></a><a name="a09da1ca77fee42e6b12a1fcb99a1bd79"></a>必须包含文件的绝对路径，如：<pre class="screen" id="s1f366c2716294b6aa3001bcefdf49a8c"><a name="s1f366c2716294b6aa3001bcefdf49a8c"></a><a name="s1f366c2716294b6aa3001bcefdf49a8c"></a>export PGSSLCRL='<em id="af59ff6d8b5df42e19f48cd38e33e6d8f"><a name="af59ff6d8b5df42e19f48cd38e33e6d8f"></a><a name="af59ff6d8b5df42e19f48cd38e33e6d8f"></a>/home/dbadmin/dws_ssl/sslcert/sslcrl-file.crl</em>'</pre>
</div>
<p id="a2d42b29a92c1423b8d72964822e22bbd"><a name="a2d42b29a92c1423b8d72964822e22bbd"></a><a name="a2d42b29a92c1423b8d72964822e22bbd"></a><strong id="ae96ba33130f348829f1179a60850469d"><a name="ae96ba33130f348829f1179a60850469d"></a><a name="ae96ba33130f348829f1179a60850469d"></a>默认值：</strong>空</p>
</td>
</tr>
</tbody>
</table>

