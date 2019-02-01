# REST API介绍<a name="zh-cn_topic_0048802577"></a>

公有云API符合RESTful API设计理论。REST从资源的角度观察整个网络，分布在各处的资源由URI（Uniform Resource Identifier）确定，客户端的应用通过URL（Unified Resource Locator）获取资源。URL的一般格式为：https://Endpoint/uri。其中uri为资源路径，也即API访问的路径。

公有云接口采用HTTPS传输协议，请求/响应报文使用JSON报文，媒体类型表示为Application/json。

DWS提供REST（Representational State Transfer）API。

REST从资源的角度来观察整个网络，提供创建、查询、更新、删除等方法访问服务的集群、快照等资源。

REST API请求/响应对可以分为五个部分：

-   [请求URI](#s0e429f59f809469cbd9f8cdada056363)
-   [请求消息头](#s450ac07b73ee4d5f80a4c2eceab745c0)
-   [请求消息体（可选）](#sad0cc096ac694c9c828c85e815c775ea)
-   [响应消息头](#s8033e231c9a9485f8a89c1f45b783a87)
-   [响应消息体（可选）](#s943c71e7c8884741a1608c9d95b87f92)

## 请求URI<a name="s0e429f59f809469cbd9f8cdada056363"></a>

请求URI由如下部分组成。

**\{URI-scheme\}://\{**Endpoint**\}/\{resource-path\}?\{query-string\}**

尽管请求URI包含在请求消息头中，但大多数语言或框架都要求您从请求消息中单独传递它，所以我们在此单独拿出来强调。

**表 1**  URI中的参数说明

<a name="t481a857ad5ae4c55831ab60fb53a30d8"></a>
<table><thead align="left"><tr id="r1ea76d1b7cdf427d976101eb9b8340ad"><th class="cellrowborder" valign="top" width="24.529999999999998%" id="mcps1.2.3.1.1"><p id="aada0df481d49466d9bcd4a543bad8a6a"><a name="aada0df481d49466d9bcd4a543bad8a6a"></a><a name="aada0df481d49466d9bcd4a543bad8a6a"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="75.47%" id="mcps1.2.3.1.2"><p id="acf8602c502a54d78bf20e6ffa908242c"><a name="acf8602c502a54d78bf20e6ffa908242c"></a><a name="acf8602c502a54d78bf20e6ffa908242c"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="rf7a44eb7335842ec95249ff26f44bea4"><td class="cellrowborder" valign="top" width="24.529999999999998%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0091558233_p136991001517"><a name="zh-cn_topic_0091558233_p136991001517"></a><a name="zh-cn_topic_0091558233_p136991001517"></a>URI-scheme</p>
</td>
<td class="cellrowborder" valign="top" width="75.47%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0091558233_p56992017520"><a name="zh-cn_topic_0091558233_p56992017520"></a><a name="zh-cn_topic_0091558233_p56992017520"></a>表示用于传输请求的协议。DWS的API都必须采用https。</p>
</td>
</tr>
<tr id="r0a6857d6fe6d4fce8d6be92ac2d85ac4"><td class="cellrowborder" valign="top" width="24.529999999999998%" headers="mcps1.2.3.1.1 "><p id="a401f5fffdbb74832aefd02ed62b12d06"><a name="a401f5fffdbb74832aefd02ed62b12d06"></a><a name="a401f5fffdbb74832aefd02ed62b12d06"></a>Endpoint</p>
</td>
<td class="cellrowborder" valign="top" width="75.47%" headers="mcps1.2.3.1.2 "><p id="p18353144310492"><a name="p18353144310492"></a><a name="p18353144310492"></a>指定承载REST服务端点的服务器域名或IP，从<a href="http://developer.huaweicloud.com/endpoint?DWS" target="_blank" rel="noopener noreferrer">地区和终端节点</a>获取。</p>
</td>
</tr>
<tr id="rd2d49f3e7b1d438caf6ab53cce66ec97"><td class="cellrowborder" valign="top" width="24.529999999999998%" headers="mcps1.2.3.1.1 "><p id="a5b75990f065c4b7b896eeb4e557c021b"><a name="a5b75990f065c4b7b896eeb4e557c021b"></a><a name="a5b75990f065c4b7b896eeb4e557c021b"></a>resource-path</p>
</td>
<td class="cellrowborder" valign="top" width="75.47%" headers="mcps1.2.3.1.2 "><p id="abf194a57d125451ebfc7409a9229bfe7"><a name="abf194a57d125451ebfc7409a9229bfe7"></a><a name="abf194a57d125451ebfc7409a9229bfe7"></a>资源路径，也即API访问路径。从具体接口的URI模块获取，例如“v3/auth/tokens”。</p>
</td>
</tr>
<tr id="r61990e7fa5204b8faf9a648efad2457b"><td class="cellrowborder" valign="top" width="24.529999999999998%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0091558233_p393966455"><a name="zh-cn_topic_0091558233_p393966455"></a><a name="zh-cn_topic_0091558233_p393966455"></a>query-string</p>
</td>
<td class="cellrowborder" valign="top" width="75.47%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0091558233_p159401867517"><a name="zh-cn_topic_0091558233_p159401867517"></a><a name="zh-cn_topic_0091558233_p159401867517"></a>可选参数，例如API版本或资源选择标准。</p>
</td>
</tr>
</tbody>
</table>

## 请求消息头<a name="s450ac07b73ee4d5f80a4c2eceab745c0"></a>

请求消息头包含如下两部分。

-   HTTP方法（也称为操作或动词），它告诉服务你正在请求什么类型的操作。DWS的REST API支持的方法如下[表2](#t584ae52eaee84b6d93c8752654189869)所示。

    **表 2**  HTTP方法

    <a name="t584ae52eaee84b6d93c8752654189869"></a>
    <table><thead align="left"><tr id="re3bff611403b4744b7de74d161792758"><th class="cellrowborder" valign="top" width="18%" id="mcps1.2.3.1.1"><p id="a4f485b874f104eea9bc7469769608b3b"><a name="a4f485b874f104eea9bc7469769608b3b"></a><a name="a4f485b874f104eea9bc7469769608b3b"></a>方法</p>
    </th>
    <th class="cellrowborder" valign="top" width="82%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0091558233_p672872219161"><a name="zh-cn_topic_0091558233_p672872219161"></a><a name="zh-cn_topic_0091558233_p672872219161"></a>说明</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="rd031571604f24944a45a0fa45e1ece65"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="a162938b535f64333beff2b8cea8ca189"><a name="a162938b535f64333beff2b8cea8ca189"></a><a name="a162938b535f64333beff2b8cea8ca189"></a>GET</p>
    </td>
    <td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="af477a6d15b2641a0a1bba5acb53ef400"><a name="af477a6d15b2641a0a1bba5acb53ef400"></a><a name="af477a6d15b2641a0a1bba5acb53ef400"></a>请求服务器返回指定资源。</p>
    </td>
    </tr>
    <tr id="r2d7aeca7bb1746b79fd325b771c26173"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="a81bbf378f80d46f8a12727a1e4222c2c"><a name="a81bbf378f80d46f8a12727a1e4222c2c"></a><a name="a81bbf378f80d46f8a12727a1e4222c2c"></a>PUT</p>
    </td>
    <td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="a5f54419046704978b9e6214361c2ac80"><a name="a5f54419046704978b9e6214361c2ac80"></a><a name="a5f54419046704978b9e6214361c2ac80"></a>请求服务器更新指定资源。</p>
    </td>
    </tr>
    <tr id="r59196097587249d0a18e85b21c5f191a"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0091558233_p472820225166"><a name="zh-cn_topic_0091558233_p472820225166"></a><a name="zh-cn_topic_0091558233_p472820225166"></a>POST</p>
    </td>
    <td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0091558233_p272812212161"><a name="zh-cn_topic_0091558233_p272812212161"></a><a name="zh-cn_topic_0091558233_p272812212161"></a>请求服务器新增资源或执行特殊操作。</p>
    </td>
    </tr>
    <tr id="re9a9d99d9648420fb4bbc4df8f7db68c"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="a4a31d40901f847d48b27a87ca416038d"><a name="a4a31d40901f847d48b27a87ca416038d"></a><a name="a4a31d40901f847d48b27a87ca416038d"></a>DELETE</p>
    </td>
    <td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="a5d75133a7e7548e9bcbfc1da4bf56df8"><a name="a5d75133a7e7548e9bcbfc1da4bf56df8"></a><a name="a5d75133a7e7548e9bcbfc1da4bf56df8"></a>请求服务器删除指定资源，如删除对象等。</p>
    </td>
    </tr>
    <tr id="rb48a231e620843c6b9b1c2033dae8704"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="a9c6329efe7c542e5bf84b4fcb6fe90c4"><a name="a9c6329efe7c542e5bf84b4fcb6fe90c4"></a><a name="a9c6329efe7c542e5bf84b4fcb6fe90c4"></a>HEAD</p>
    </td>
    <td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0091558233_p42261787492"><a name="zh-cn_topic_0091558233_p42261787492"></a><a name="zh-cn_topic_0091558233_p42261787492"></a>请求服务器资源头部。</p>
    </td>
    </tr>
    <tr id="rc4f49f3481304b24ab2979c0273c183f"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="a52c32afd923e40f59ee426e5837190ea"><a name="a52c32afd923e40f59ee426e5837190ea"></a><a name="a52c32afd923e40f59ee426e5837190ea"></a>PATCH</p>
    </td>
    <td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="afb58551ba965404f886ed23d1644be0f"><a name="afb58551ba965404f886ed23d1644be0f"></a><a name="afb58551ba965404f886ed23d1644be0f"></a>请求服务器更新资源的部分内容。</p>
    <p id="aca99627670294f3c81daa35375b46f12"><a name="aca99627670294f3c81daa35375b46f12"></a><a name="aca99627670294f3c81daa35375b46f12"></a>当资源不存在的时候，PATCH可能会去创建一个新的资源。</p>
    </td>
    </tr>
    </tbody>
    </table>

-   可选的附加请求头字段，如指定的URI和HTTP方法所要求的字段。详细的公共请求消息头字段请参见[表3](#t6dd8d2d3a6694f2fbebfdf810fc86819)。

    **表 3**  公共请求消息头

    <a name="t6dd8d2d3a6694f2fbebfdf810fc86819"></a>
    <table><thead align="left"><tr id="row1123991114352"><th class="cellrowborder" valign="top" width="19.74%" id="mcps1.2.5.1.1"><p id="p024517114357"><a name="p024517114357"></a><a name="p024517114357"></a>名称</p>
    </th>
    <th class="cellrowborder" valign="top" width="26.490000000000002%" id="mcps1.2.5.1.2"><p id="p924813113355"><a name="p924813113355"></a><a name="p924813113355"></a>描述</p>
    </th>
    <th class="cellrowborder" valign="top" width="19.93%" id="mcps1.2.5.1.3"><p id="p4251181193511"><a name="p4251181193511"></a><a name="p4251181193511"></a>是否必选</p>
    </th>
    <th class="cellrowborder" valign="top" width="33.839999999999996%" id="mcps1.2.5.1.4"><p id="p112561117358"><a name="p112561117358"></a><a name="p112561117358"></a>示例</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row8315511183512"><td class="cellrowborder" valign="top" width="19.74%" headers="mcps1.2.5.1.1 "><p id="p1319111153520"><a name="p1319111153520"></a><a name="p1319111153520"></a>Content-type</p>
    </td>
    <td class="cellrowborder" valign="top" width="26.490000000000002%" headers="mcps1.2.5.1.2 "><p id="p1732715119359"><a name="p1732715119359"></a><a name="p1732715119359"></a>发送的实体的MIME类型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="19.93%" headers="mcps1.2.5.1.3 "><p id="p143314111351"><a name="p143314111351"></a><a name="p143314111351"></a>是</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.839999999999996%" headers="mcps1.2.5.1.4 "><p id="p14335141173512"><a name="p14335141173512"></a><a name="p14335141173512"></a>application/json</p>
    </td>
    </tr>
    <tr id="row6337111193515"><td class="cellrowborder" valign="top" width="19.74%" headers="mcps1.2.5.1.1 "><p id="p17341711123512"><a name="p17341711123512"></a><a name="p17341711123512"></a>Content-Length</p>
    </td>
    <td class="cellrowborder" valign="top" width="26.490000000000002%" headers="mcps1.2.5.1.2 "><p id="p93441611143510"><a name="p93441611143510"></a><a name="p93441611143510"></a>请求body长度，单位为Byte。</p>
    </td>
    <td class="cellrowborder" valign="top" width="19.93%" headers="mcps1.2.5.1.3 "><p id="p1434817119359"><a name="p1434817119359"></a><a name="p1434817119359"></a>POST/PUT请求必填。 GET不能包含。</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.839999999999996%" headers="mcps1.2.5.1.4 "><p id="p143523112353"><a name="p143523112353"></a><a name="p143523112353"></a>3495</p>
    </td>
    </tr>
    <tr id="row193543111356"><td class="cellrowborder" valign="top" width="19.74%" headers="mcps1.2.5.1.1 "><p id="p2035741193513"><a name="p2035741193513"></a><a name="p2035741193513"></a>X-Project-Id</p>
    </td>
    <td class="cellrowborder" valign="top" width="26.490000000000002%" headers="mcps1.2.5.1.2 "><p id="p16361191193510"><a name="p16361191193510"></a><a name="p16361191193510"></a>project id，用于不同project取token。</p>
    <p id="p43637114356"><a name="p43637114356"></a><a name="p43637114356"></a>如果是DeC的请求或者多project的请求则必须传入project id。</p>
    </td>
    <td class="cellrowborder" valign="top" width="19.93%" headers="mcps1.2.5.1.3 "><p id="p3366131123515"><a name="p3366131123515"></a><a name="p3366131123515"></a>否</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.839999999999996%" headers="mcps1.2.5.1.4 "><p id="p103689116359"><a name="p103689116359"></a><a name="p103689116359"></a>e9993fc787d94b6c886cbaa340f9c0f4</p>
    </td>
    </tr>
    <tr id="row15370141153515"><td class="cellrowborder" valign="top" width="19.74%" headers="mcps1.2.5.1.1 "><p id="p03731811153514"><a name="p03731811153514"></a><a name="p03731811153514"></a>X-Auth-Token</p>
    </td>
    <td class="cellrowborder" valign="top" width="26.490000000000002%" headers="mcps1.2.5.1.2 "><p id="p6376111163511"><a name="p6376111163511"></a><a name="p6376111163511"></a>用户Token。请参见<a href="Token认证.md">Token认证</a>进行获取。</p>
    </td>
    <td class="cellrowborder" valign="top" width="19.93%" headers="mcps1.2.5.1.3 "><p id="p1138091113518"><a name="p1138091113518"></a><a name="p1138091113518"></a>是</p>
    <p id="p1179346141516"><a name="p1179346141516"></a><a name="p1179346141516"></a>使用Token认证该字段必选。</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.839999999999996%" headers="mcps1.2.5.1.4 "><p id="p7384111118359"><a name="p7384111118359"></a><a name="p7384111118359"></a>-</p>
    </td>
    </tr>
    <tr id="row11386141133510"><td class="cellrowborder" valign="top" width="19.74%" headers="mcps1.2.5.1.1 "><p id="p5388211133515"><a name="p5388211133515"></a><a name="p5388211133515"></a>X-Language</p>
    </td>
    <td class="cellrowborder" valign="top" width="26.490000000000002%" headers="mcps1.2.5.1.2 "><p id="p16391101119350"><a name="p16391101119350"></a><a name="p16391101119350"></a>请求语言</p>
    </td>
    <td class="cellrowborder" valign="top" width="19.93%" headers="mcps1.2.5.1.3 "><p id="p539461143514"><a name="p539461143514"></a><a name="p539461143514"></a>否</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.839999999999996%" headers="mcps1.2.5.1.4 "><p id="p239871112358"><a name="p239871112358"></a><a name="p239871112358"></a>zh_cn</p>
    </td>
    </tr>
    </tbody>
    </table>

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >其它header属性，请遵照http协议。  


## 请求消息体（可选）<a name="sad0cc096ac694c9c828c85e815c775ea"></a>

请求消息体通常以结构化格式（如JSON或XML）发出，与请求消息头中Content-type对应，传递除请求消息头之外的内容。

## 响应消息头<a name="s8033e231c9a9485f8a89c1f45b783a87"></a>

响应消息头包含如下两部分。

-   一个HTTP状态代码，从2xx成功代码到4xx或5xx错误代码。 或者，可以返回服务定义的状态码，如API文档中所示。
-   附加响应头字段，如支持请求的响应所需，如Content-type响应消息头。详细的公共响应消息头字段请参见[表4](#t93cfeb318cec43f38968f49656e1eb2e)。

    **表 4**  响应消息头

    <a name="t93cfeb318cec43f38968f49656e1eb2e"></a>
    <table><thead align="left"><tr id="rcb0d97e0569b40739165cb857315e9a8"><th class="cellrowborder" valign="top" width="23%" id="mcps1.2.4.1.1"><p id="aa57d706953774032877626e4d148fff2"><a name="aa57d706953774032877626e4d148fff2"></a><a name="aa57d706953774032877626e4d148fff2"></a>名称</p>
    </th>
    <th class="cellrowborder" valign="top" width="44%" id="mcps1.2.4.1.2"><p id="a29f6935b52f74cc9abc4cdf563e2d8e4"><a name="a29f6935b52f74cc9abc4cdf563e2d8e4"></a><a name="a29f6935b52f74cc9abc4cdf563e2d8e4"></a>描述</p>
    </th>
    <th class="cellrowborder" valign="top" width="33%" id="mcps1.2.4.1.3"><p id="a863aee3fd4ac4055a18e56d00eb1c1e9"><a name="a863aee3fd4ac4055a18e56d00eb1c1e9"></a><a name="a863aee3fd4ac4055a18e56d00eb1c1e9"></a>示例</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="r849a573bb27d45f19172d7bc428952a6"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.1 "><p id="ac4d9b092761a4eb783669c820d89ef15"><a name="ac4d9b092761a4eb783669c820d89ef15"></a><a name="ac4d9b092761a4eb783669c820d89ef15"></a>Date</p>
    </td>
    <td class="cellrowborder" valign="top" width="44%" headers="mcps1.2.4.1.2 "><p id="a4622298f26ee47c4b8c532435e7a4e97"><a name="a4622298f26ee47c4b8c532435e7a4e97"></a><a name="a4622298f26ee47c4b8c532435e7a4e97"></a>HTTP协议标准报头。表示消息发送的时间，时间的描述格式由rfc822定义。</p>
    </td>
    <td class="cellrowborder" valign="top" width="33%" headers="mcps1.2.4.1.3 "><p id="a98ddd05cc2e74f0298ac02282d499b1a"><a name="a98ddd05cc2e74f0298ac02282d499b1a"></a><a name="a98ddd05cc2e74f0298ac02282d499b1a"></a>Mon, 12 Nov 2007 15:55:01 GMT</p>
    </td>
    </tr>
    <tr id="r8cc3cc6ad54e45608504a8ddad5092a9"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.1 "><p id="ae1669282b00446dbbb20a5d06c8ba8b1"><a name="ae1669282b00446dbbb20a5d06c8ba8b1"></a><a name="ae1669282b00446dbbb20a5d06c8ba8b1"></a>Server</p>
    </td>
    <td class="cellrowborder" valign="top" width="44%" headers="mcps1.2.4.1.2 "><p id="a8b9373b2bf034ebbb58e5996eedec3da"><a name="a8b9373b2bf034ebbb58e5996eedec3da"></a><a name="a8b9373b2bf034ebbb58e5996eedec3da"></a>HTTP协议标准报头。包含了服务器用来处理请求的软件信息。</p>
    </td>
    <td class="cellrowborder" valign="top" width="33%" headers="mcps1.2.4.1.3 "><p id="a8290996e62814d36bd0505b9ecbc5d21"><a name="a8290996e62814d36bd0505b9ecbc5d21"></a><a name="a8290996e62814d36bd0505b9ecbc5d21"></a>Apache</p>
    </td>
    </tr>
    <tr id="r74e598c2548842378a7f46796501eaa6"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.1 "><p id="a98e1303132884da7904e73626ba954ee"><a name="a98e1303132884da7904e73626ba954ee"></a><a name="a98e1303132884da7904e73626ba954ee"></a>Content-Length</p>
    </td>
    <td class="cellrowborder" valign="top" width="44%" headers="mcps1.2.4.1.2 "><p id="a10c5d03390c747ef958c74707c6f6314"><a name="a10c5d03390c747ef958c74707c6f6314"></a><a name="a10c5d03390c747ef958c74707c6f6314"></a>HTTP协议标准报头。用于指明实体正文的长度，以字节方式存储的十进制数字来表示。</p>
    </td>
    <td class="cellrowborder" valign="top" width="33%" headers="mcps1.2.4.1.3 "><p id="af416cb381db945f6b49a0ddcb67005ab"><a name="af416cb381db945f6b49a0ddcb67005ab"></a><a name="af416cb381db945f6b49a0ddcb67005ab"></a>-</p>
    </td>
    </tr>
    <tr id="rdf5dd6e315be4e7aa46fd1ab0724f267"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.1 "><p id="a941744543a294a36add770586439f94e"><a name="a941744543a294a36add770586439f94e"></a><a name="a941744543a294a36add770586439f94e"></a>Content-Type</p>
    </td>
    <td class="cellrowborder" valign="top" width="44%" headers="mcps1.2.4.1.2 "><p id="a7ad6ca1b1b4c483db3c6d2ef9e1de09d"><a name="a7ad6ca1b1b4c483db3c6d2ef9e1de09d"></a><a name="a7ad6ca1b1b4c483db3c6d2ef9e1de09d"></a>HTTP协议标准报头。用于指明发送给接收者的实体正文的媒体类型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="33%" headers="mcps1.2.4.1.3 "><p id="abc0a938f3151487ea21d37c6b61cb5be"><a name="abc0a938f3151487ea21d37c6b61cb5be"></a><a name="abc0a938f3151487ea21d37c6b61cb5be"></a>application/json</p>
    </td>
    </tr>
    </tbody>
    </table>


## 响应消息体（可选）<a name="s943c71e7c8884741a1608c9d95b87f92"></a>

响应消息体通常以结构化格式（如JSON或XML）返回，与响应消息头中Content-type对应，传递除响应消息头之外的内容。

## 发起请求<a name="sf0eeadd53fd74f3e921b247382fac764"></a>

共有三种方式可以基于已构建好的请求消息发起请求，分别为：

-   cURL

    cURL是一个命令行工具，用来执行各种URL操作和信息传输。cURL充当的是HTTP客户端，可以发送HTTP请求给服务端，并接收响应消息。cURL适用于接口调试。关于cURL详细信息请参见[https://curl.haxx.se/](https://curl.haxx.se/)。

-   编码

    通过编码调用接口，组装请求消息，并发送处理请求消息。

-   REST客户端

    Mozilla、Google都为REST提供了图形化的浏览器插件，发送处理请求消息。针对Firefox，请参见[Firefox REST Client](https://addons.mozilla.org/en-US/firefox/addon/restclient/)。针对Chrome，请参见[Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)。


