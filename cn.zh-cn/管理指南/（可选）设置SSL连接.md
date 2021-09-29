# （可选）设置SSL连接<a name="ZH-CN_TOPIC_0000001145696643"></a>

GaussDB\(DWS\) 支持SSL认证方式的连接，以加密GaussDB\(DWS\) 客户端与数据库之间传输的数据。SSL连接方式的安全性高于普通模式，集群默认开启SSL功能允许来自客户端的SSL连接或非SSL连接，从安全性考虑，建议用户在客户端使用SSL连接方式。如果要强制使用SSL连接，需要为集群开启“服务器端是否强制使用SSL连接“。

在集群的“安全设置“页面可以设置是否开启“服务器端是否强制使用SSL连接“。

>![](public_sys-resources/icon-note.gif) **说明：** 
>-   修改安全配置参数并保存生效可能需要重启集群，将导致集群暂时不可用。
>-   实时数仓暂不支持SSL连接。
>-   实时数仓暂不支持MRS数据源连接。
>-   修改集群安全配置必须同时满足以下两个条件：
>    -   集群状态为“可用“或“非均衡“。
>    -   任务信息不能处于“创建快照中“、“节点扩容“、“配置中“或“重启中“。

本章节为您介绍以下内容：

-   [设置SSL连接](#section478703071283)
-   [客户端和服务器端SSL连接参数组合情况](#section1916311515557)

## 设置SSL连接<a name="section478703071283"></a>

1.  登录GaussDB\(DWS\) 管理控制台。
2.  在左侧导航树中，单击“集群管理“。
3.  在集群列表中，单击指定集群的名称，然后单击“安全设置“。

    默认显示“配置状态“为“已同步“，表示页面显示的是数据库当前最新结果。

4.  在“SSL连接“区域中，单击“服务器端是否强制使用SSL连接“的设置开关进行设置，建议开启。

    ![](figures/dws_icon_on.png)：开启，表示服务器端强制要求SSL连接。

    ![](figures/dws_icon_off.png)：关闭，表示服务器端对是否通过SSL连接不作强制要求，默认为关闭。

    **图 1**  SSL连接<a name="fig168181335124718"></a>  
    ![](figures/SSL连接.png "SSL连接")

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   如果使用GaussDB\(DWS\) 提供的gsql客户端或ODBC驱动，GaussDB\(DWS\) 支持的SSL协议为TLSv1.2。
    >-   如果使用GaussDB\(DWS\) 提供的JDBC驱动，支持的SSL协议有SSLv3、TLSv1、TLSv1.1、TLSv1.2。客户端与数据库之间实际使用何种SSL协议，依赖客户端使用的JDK（Java Development Kit）版本，一般JDK支持多个SSL协议。

5.  单击“应用“。

    系统将自动应用保存SSL连接设置，在“安全设置“页面，“配置状态“显示“应用中“。当“配置状态“显示为“已同步“，表示配置已保存生效。


## 客户端和服务器端SSL连接参数组合情况<a name="section1916311515557"></a>

客户端最终是否使用SSL加密连接方式、是否验证服务器证书，取决于客户端参数sslmode与服务器端（即GaussDB\(DWS\) 集群侧）参数ssl、require\_ssl。参数说明如下：

-   **ssl（服务器）**

    ssl参数表示是否开启SSL功能。on表示开启，off表示关闭。

    -   对于集群版本高于1.3.1（包括1.3.1）的集群，默认为on，不支持在GaussDB\(DWS\) 管理控制台上设置。
    -   对于集群版本低于1.3.1的集群，默认为on。ssl参数可通过GaussDB\(DWS\) 管理控制台上集群的“安全设置“页面中的“SSL连接“进行设置。

-   **require\_ssl（服务器）**

    require\_ssl参数是设置服务器端是否强制要求SSL连接，该参数只有当ssl为on时才有效。on表示服务器端强制要求SSL连接。off表示服务器端对是否通过SSL连接不作强制要求。

    -   对于集群版本高于1.3.1（包括1.3.1）的集群，默认为off。require\_ssl参数可通过GaussDB\(DWS\) 管理控制台上集群的“安全设置“页面中的“服务器端是否强制使用SSL连接“进行设置。
    -   对于集群版本低于1.3.1的集群，默认为off，不支持在GaussDB\(DWS\) 管理控制台上设置。

-   **sslmode（客户端）**

    可在SQL客户端工具中进行设置。

    -   在gsql命令行客户端中，为“PGSSLMODE“参数。
    -   在Data Studio客户端中，为“SSL模式“参数。


客户端参数sslmode与服务器端参数ssl、require\_ssl配置组合结果如下：

**表 1**  客户端与服务器端SSL参数组合结果

<a name="table15451139114317"></a>
<table><thead align="left"><tr id="r355add9c9a7f41bda915ac600dac576c"><th class="cellrowborder" valign="top" width="10.66%" id="mcps1.2.5.1.1"><p id="a7b70a0fb1cf54e2b9f5a848f2f620524"><a name="a7b70a0fb1cf54e2b9f5a848f2f620524"></a><a name="a7b70a0fb1cf54e2b9f5a848f2f620524"></a>ssl（服务器）</p>
</th>
<th class="cellrowborder" valign="top" width="14.85%" id="mcps1.2.5.1.2"><p id="af54a777133684c8d88584ba3c148d570"><a name="af54a777133684c8d88584ba3c148d570"></a><a name="af54a777133684c8d88584ba3c148d570"></a>sslmode（客户端）</p>
</th>
<th class="cellrowborder" valign="top" width="17.119999999999997%" id="mcps1.2.5.1.3"><p id="a4f4b48b5c8c94c01ba3cebcd3f604899"><a name="a4f4b48b5c8c94c01ba3cebcd3f604899"></a><a name="a4f4b48b5c8c94c01ba3cebcd3f604899"></a>require_ssl（服务器）</p>
</th>
<th class="cellrowborder" valign="top" width="57.37%" id="mcps1.2.5.1.4"><p id="a8b5c97f6e3eb452c938c6a2cff74c38f"><a name="a8b5c97f6e3eb452c938c6a2cff74c38f"></a><a name="a8b5c97f6e3eb452c938c6a2cff74c38f"></a>结果</p>
</th>
</tr>
</thead>
<tbody><tr id="r62ddf2bbc75b4079b1a2ec62f0692d6b"><td class="cellrowborder" rowspan="10" valign="top" width="10.66%" headers="mcps1.2.5.1.1 "><p id="a3e78fc2918b34a6f8a717dde92f3fc2a"><a name="a3e78fc2918b34a6f8a717dde92f3fc2a"></a><a name="a3e78fc2918b34a6f8a717dde92f3fc2a"></a>on</p>
</td>
<td class="cellrowborder" valign="top" width="14.85%" headers="mcps1.2.5.1.2 "><p id="a33fee70f27ae4b91a31daa855b8ed9a0"><a name="a33fee70f27ae4b91a31daa855b8ed9a0"></a><a name="a33fee70f27ae4b91a31daa855b8ed9a0"></a>disable</p>
</td>
<td class="cellrowborder" valign="top" width="17.119999999999997%" headers="mcps1.2.5.1.3 "><p id="a8e8d0be8175d47918d0829af2781e983"><a name="a8e8d0be8175d47918d0829af2781e983"></a><a name="a8e8d0be8175d47918d0829af2781e983"></a>on</p>
</td>
<td class="cellrowborder" valign="top" width="57.37%" headers="mcps1.2.5.1.4 "><p id="adabec5d250d2412bb0eeca24199da945"><a name="adabec5d250d2412bb0eeca24199da945"></a><a name="adabec5d250d2412bb0eeca24199da945"></a>由于服务器端要求使用 SSL，但客户端针对该连接禁用了 SSL，因此无法建立连接。</p>
</td>
</tr>
<tr id="rd1415aba4c6141cc8d4a9d9ee74dc80d"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="a25f23ee3007f4fcc9044b75afd7c9954"><a name="a25f23ee3007f4fcc9044b75afd7c9954"></a><a name="a25f23ee3007f4fcc9044b75afd7c9954"></a>disable</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="a665fb82ed5de4de09ea9be0553daedab"><a name="a665fb82ed5de4de09ea9be0553daedab"></a><a name="a665fb82ed5de4de09ea9be0553daedab"></a>off</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="a86de0a2f9a5049c083cfd07ec10153a1"><a name="a86de0a2f9a5049c083cfd07ec10153a1"></a><a name="a86de0a2f9a5049c083cfd07ec10153a1"></a>连接未加密。</p>
</td>
</tr>
<tr id="r9eb0e52c41d74b10b9c2c0b486f513dd"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="a7131377f60394c7a9e3b19c6171dd019"><a name="a7131377f60394c7a9e3b19c6171dd019"></a><a name="a7131377f60394c7a9e3b19c6171dd019"></a>allow</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="af9962f4ead2a4f158e2028064e8fa4ef"><a name="af9962f4ead2a4f158e2028064e8fa4ef"></a><a name="af9962f4ead2a4f158e2028064e8fa4ef"></a>on</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="ab8d0f618c92a4140a9c1d9eae41b8ae9"><a name="ab8d0f618c92a4140a9c1d9eae41b8ae9"></a><a name="ab8d0f618c92a4140a9c1d9eae41b8ae9"></a>连接经过加密。</p>
</td>
</tr>
<tr id="r647075f1e10c4c198317ecd0b83aca5c"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="aa0eee6d2caa049709669990d5430ebb7"><a name="aa0eee6d2caa049709669990d5430ebb7"></a><a name="aa0eee6d2caa049709669990d5430ebb7"></a>allow</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="ad4739683696e4954afad8c5bcc52901c"><a name="ad4739683696e4954afad8c5bcc52901c"></a><a name="ad4739683696e4954afad8c5bcc52901c"></a>off</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="ab4c8bb6ca01a4bd5bbae27bc36e0788d"><a name="ab4c8bb6ca01a4bd5bbae27bc36e0788d"></a><a name="ab4c8bb6ca01a4bd5bbae27bc36e0788d"></a>连接未加密。</p>
</td>
</tr>
<tr id="r19c24691a02e4d328d0bd356da8767d5"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="aa9cb9ff881e9432683e93016dd10b6da"><a name="aa9cb9ff881e9432683e93016dd10b6da"></a><a name="aa9cb9ff881e9432683e93016dd10b6da"></a>prefer</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="a480653a387d44a67a72fc6ccfa586eee"><a name="a480653a387d44a67a72fc6ccfa586eee"></a><a name="a480653a387d44a67a72fc6ccfa586eee"></a>on</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="a4bda372df21844e5b891ae07b3acefe6"><a name="a4bda372df21844e5b891ae07b3acefe6"></a><a name="a4bda372df21844e5b891ae07b3acefe6"></a>连接经过加密。</p>
</td>
</tr>
<tr id="racc4977e5ce341e79fb08358ab9b8c2d"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="a4891f1b8e4c744c3b1c2358f1b6b70a1"><a name="a4891f1b8e4c744c3b1c2358f1b6b70a1"></a><a name="a4891f1b8e4c744c3b1c2358f1b6b70a1"></a>prefer</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="a9422603a15e14af08884d086d5fb18b5"><a name="a9422603a15e14af08884d086d5fb18b5"></a><a name="a9422603a15e14af08884d086d5fb18b5"></a>off</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="a128e4e83906246a08e3ca36a1c737b49"><a name="a128e4e83906246a08e3ca36a1c737b49"></a><a name="a128e4e83906246a08e3ca36a1c737b49"></a>连接经过加密。</p>
</td>
</tr>
<tr id="r15f4c4a8ebb14afbafa099d85ef39298"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="a9a9746a997944cee8349e6751c5e7099"><a name="a9a9746a997944cee8349e6751c5e7099"></a><a name="a9a9746a997944cee8349e6751c5e7099"></a>require</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="a51a659efccb84491b56a756c7213fc33"><a name="a51a659efccb84491b56a756c7213fc33"></a><a name="a51a659efccb84491b56a756c7213fc33"></a>on</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="ad1da2821861d4f74807b2a231d74f776"><a name="ad1da2821861d4f74807b2a231d74f776"></a><a name="ad1da2821861d4f74807b2a231d74f776"></a>连接经过加密。</p>
</td>
</tr>
<tr id="re3cb0b7aa7d147e8b9cddc4f8772e588"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="a3ee91e2d35d447abaaa654fdfb2c1cda"><a name="a3ee91e2d35d447abaaa654fdfb2c1cda"></a><a name="a3ee91e2d35d447abaaa654fdfb2c1cda"></a>require</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="a2417da5d11b34e6eb22c5e23abd964a8"><a name="a2417da5d11b34e6eb22c5e23abd964a8"></a><a name="a2417da5d11b34e6eb22c5e23abd964a8"></a>off</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="af733535d0a3547708898d100034ead60"><a name="af733535d0a3547708898d100034ead60"></a><a name="af733535d0a3547708898d100034ead60"></a>连接经过加密。</p>
</td>
</tr>
<tr id="r6ad7de0dd0c14d2a9da79957f8e88a0c"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="a7248e51cabc84b38927a8523b6f21137"><a name="a7248e51cabc84b38927a8523b6f21137"></a><a name="a7248e51cabc84b38927a8523b6f21137"></a>verify-ca</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="ad1897b8a87a94fd69a4f1140c5898813"><a name="ad1897b8a87a94fd69a4f1140c5898813"></a><a name="ad1897b8a87a94fd69a4f1140c5898813"></a>on</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="a74366920fd6447d49377258bf6b1b264"><a name="a74366920fd6447d49377258bf6b1b264"></a><a name="a74366920fd6447d49377258bf6b1b264"></a>连接经过加密，且验证了服务器证书。</p>
</td>
</tr>
<tr id="rc33abe03abec4a2a8f57d3d3a64d7be3"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="a80805b432a4f4eea8cc86766f78b2d15"><a name="a80805b432a4f4eea8cc86766f78b2d15"></a><a name="a80805b432a4f4eea8cc86766f78b2d15"></a>verify-ca</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="a483b735d07a04335a08e3cab6f92a97a"><a name="a483b735d07a04335a08e3cab6f92a97a"></a><a name="a483b735d07a04335a08e3cab6f92a97a"></a>off</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="a264a3332f3944e9a9f2b34db9b345b21"><a name="a264a3332f3944e9a9f2b34db9b345b21"></a><a name="a264a3332f3944e9a9f2b34db9b345b21"></a>连接经过加密，且验证了服务器证书。</p>
</td>
</tr>
<tr id="rf72d3e2843934cd9b8dd59548cd3be1c"><td class="cellrowborder" rowspan="10" valign="top" width="10.66%" headers="mcps1.2.5.1.1 "><p id="a217430f24485439393825ecceec13e0c"><a name="a217430f24485439393825ecceec13e0c"></a><a name="a217430f24485439393825ecceec13e0c"></a>off</p>
</td>
<td class="cellrowborder" valign="top" width="14.85%" headers="mcps1.2.5.1.2 "><p id="a07fb6a03fd5a4007bd85a6328c4a9c6b"><a name="a07fb6a03fd5a4007bd85a6328c4a9c6b"></a><a name="a07fb6a03fd5a4007bd85a6328c4a9c6b"></a>disable</p>
</td>
<td class="cellrowborder" valign="top" width="17.119999999999997%" headers="mcps1.2.5.1.3 "><p id="a6034b6a1a82a4d9e8e789e5d34d2d8b2"><a name="a6034b6a1a82a4d9e8e789e5d34d2d8b2"></a><a name="a6034b6a1a82a4d9e8e789e5d34d2d8b2"></a>on</p>
</td>
<td class="cellrowborder" valign="top" width="57.37%" headers="mcps1.2.5.1.4 "><p id="a9e933492038b455a9d32758cb7933c32"><a name="a9e933492038b455a9d32758cb7933c32"></a><a name="a9e933492038b455a9d32758cb7933c32"></a>连接未加密。</p>
</td>
</tr>
<tr id="re61e3ac813784038a929a41f4575f52f"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="a889b21370a404bd4858140173ed02376"><a name="a889b21370a404bd4858140173ed02376"></a><a name="a889b21370a404bd4858140173ed02376"></a>disable</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="a6b83c26f620f403b8c575243b1f75513"><a name="a6b83c26f620f403b8c575243b1f75513"></a><a name="a6b83c26f620f403b8c575243b1f75513"></a>off</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="a078607c627c640079c7072c634fc362d"><a name="a078607c627c640079c7072c634fc362d"></a><a name="a078607c627c640079c7072c634fc362d"></a>连接未加密。</p>
</td>
</tr>
<tr id="r954d308f6bd043beb3ea0ef02ce60721"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="a1c8ac46fc0c24cf68ce77d2a7f60c7e1"><a name="a1c8ac46fc0c24cf68ce77d2a7f60c7e1"></a><a name="a1c8ac46fc0c24cf68ce77d2a7f60c7e1"></a>allow</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="abe34e8f39ad24a4ea9a2649d00bb8ec9"><a name="abe34e8f39ad24a4ea9a2649d00bb8ec9"></a><a name="abe34e8f39ad24a4ea9a2649d00bb8ec9"></a>on</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="afa8a5bb9f3114e43bcb5fa9b0e68faad"><a name="afa8a5bb9f3114e43bcb5fa9b0e68faad"></a><a name="afa8a5bb9f3114e43bcb5fa9b0e68faad"></a>连接未加密。</p>
</td>
</tr>
<tr id="rad2d9b9a419042599a3742e0f4c64b9f"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="aa1db3dde5ffe46f29bf2ac88e0af8528"><a name="aa1db3dde5ffe46f29bf2ac88e0af8528"></a><a name="aa1db3dde5ffe46f29bf2ac88e0af8528"></a>allow</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="a18671a2e86c24c9093ecc0f070d5cec7"><a name="a18671a2e86c24c9093ecc0f070d5cec7"></a><a name="a18671a2e86c24c9093ecc0f070d5cec7"></a>off</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="a23067107fce2405899e18da68f250634"><a name="a23067107fce2405899e18da68f250634"></a><a name="a23067107fce2405899e18da68f250634"></a>连接未加密。</p>
</td>
</tr>
<tr id="rbe2f3d97ccda4da7a94bd8aaea8c7c36"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="a9f5bd8414de046b9b2ee868314e3bd58"><a name="a9f5bd8414de046b9b2ee868314e3bd58"></a><a name="a9f5bd8414de046b9b2ee868314e3bd58"></a>prefer</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="a44de2784e3c94135a54e65e76e0c54cc"><a name="a44de2784e3c94135a54e65e76e0c54cc"></a><a name="a44de2784e3c94135a54e65e76e0c54cc"></a>on</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="a54497bbf08d647738ef678f5616489a5"><a name="a54497bbf08d647738ef678f5616489a5"></a><a name="a54497bbf08d647738ef678f5616489a5"></a>连接未加密。</p>
</td>
</tr>
<tr id="rb3edfcc877a940968323e421099419d4"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="ab3790c4c627447d5badb67c8688913dc"><a name="ab3790c4c627447d5badb67c8688913dc"></a><a name="ab3790c4c627447d5badb67c8688913dc"></a>prefer</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="af831647acfb845f6a9e4cd4aa95c295b"><a name="af831647acfb845f6a9e4cd4aa95c295b"></a><a name="af831647acfb845f6a9e4cd4aa95c295b"></a>off</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="a5f855c85aade49e8a36bf05255ed55f6"><a name="a5f855c85aade49e8a36bf05255ed55f6"></a><a name="a5f855c85aade49e8a36bf05255ed55f6"></a>连接未加密。</p>
</td>
</tr>
<tr id="r2632f81144f9406a87a2cc6c89011d82"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="ac35bbd9317c9416ab238cc122ce97d47"><a name="ac35bbd9317c9416ab238cc122ce97d47"></a><a name="ac35bbd9317c9416ab238cc122ce97d47"></a>require</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="a6e6e3cfa03d64e4abf4fc3995ae646f3"><a name="a6e6e3cfa03d64e4abf4fc3995ae646f3"></a><a name="a6e6e3cfa03d64e4abf4fc3995ae646f3"></a>on</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="adfac91a6ac2246b0bb27b06c636dc232"><a name="adfac91a6ac2246b0bb27b06c636dc232"></a><a name="adfac91a6ac2246b0bb27b06c636dc232"></a>由于客户端要求使用 SSL，但服务器端禁用了 SSL，因此无法建立连接。</p>
</td>
</tr>
<tr id="r1e457ea33fec4cac9e77887ffdf27622"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="a29780e72f6c34caf8d1e89edd7a3dd19"><a name="a29780e72f6c34caf8d1e89edd7a3dd19"></a><a name="a29780e72f6c34caf8d1e89edd7a3dd19"></a>require</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="a7a2cd8bc207c4849964f69d1c05d898b"><a name="a7a2cd8bc207c4849964f69d1c05d898b"></a><a name="a7a2cd8bc207c4849964f69d1c05d898b"></a>off</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="a1053e4dc3c5c4c5885d7c49c82a21623"><a name="a1053e4dc3c5c4c5885d7c49c82a21623"></a><a name="a1053e4dc3c5c4c5885d7c49c82a21623"></a>由于客户端要求使用 SSL，但服务器端禁用了 SSL，因此无法建立连接。</p>
</td>
</tr>
<tr id="rf8ca62c481a3440d96e3be781d3c3da8"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="a29a9174257c84b0e97d85d9bc7467bac"><a name="a29a9174257c84b0e97d85d9bc7467bac"></a><a name="a29a9174257c84b0e97d85d9bc7467bac"></a>verify-ca</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="aaea7b0943815449085e4317001a96c5b"><a name="aaea7b0943815449085e4317001a96c5b"></a><a name="aaea7b0943815449085e4317001a96c5b"></a>on</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="a6fe94346112f44d99e3509134ee3bc6d"><a name="a6fe94346112f44d99e3509134ee3bc6d"></a><a name="a6fe94346112f44d99e3509134ee3bc6d"></a>由于客户端要求使用 SSL，但服务器端禁用了 SSL，因此无法建立连接。</p>
</td>
</tr>
<tr id="rb81f0e36ee9b4433a08a6df14f302ff9"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="a04d6064a2900404dbefd08bc70081503"><a name="a04d6064a2900404dbefd08bc70081503"></a><a name="a04d6064a2900404dbefd08bc70081503"></a>verify-ca</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="aa46206d00ff042dcb6e3054447adaa5c"><a name="aa46206d00ff042dcb6e3054447adaa5c"></a><a name="aa46206d00ff042dcb6e3054447adaa5c"></a>off</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="a3974806634b94ce49ae43e69f48fa246"><a name="a3974806634b94ce49ae43e69f48fa246"></a><a name="a3974806634b94ce49ae43e69f48fa246"></a>由于客户端要求使用 SSL，但服务器端禁用了 SSL，因此无法建立连接。</p>
</td>
</tr>
</tbody>
</table>

