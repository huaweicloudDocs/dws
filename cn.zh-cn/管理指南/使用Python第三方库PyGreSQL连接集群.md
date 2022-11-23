# 使用Python第三方库PyGreSQL连接集群<a name="ZH-CN_TOPIC_0000001455917021"></a>

用户在创建好数据仓库集群后使用PyGreSQL第三方库连接到集群，则可以使用Python访问GaussDB\(DWS\) ，并进行数据表的各类操作。

## 连接集群前的准备<a name="section5781841515252"></a>

-   GaussDB\(DWS\) 集群已绑定弹性IP。
-   已获取GaussDB\(DWS\) 集群的数据库管理员用户名和密码。

    请注意，由于MD5算法已经被证实存在碰撞可能，已严禁将之用于密码校验算法。当前GaussDB\(DWS\) 采用默认安全设计，默认禁止MD5算法的密码校验，可能导致开源客户端无法正常连接的问题。建议先检查一下数据库参数password\_encryption\_type参数是否为1，如果取值不为1，需要修改，修改方法参见[修改数据库参数](https://support.huaweicloud.com/mgtg-dws/dws_01_0152.html)；然后修改一次准备使用的数据库用户的密码。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   当前GaussDB\(DWS\)出于安全考虑，已经默认不再使用MD5存储密码摘要了，这将导致使用开源驱动或者客户端无法正常连接数据库。需要您调整一下密码策略后再创建一个新用户或者对老用户做一次密码修改，方可使用开源协议中使用的MD5认证算法。
    >-   数据库中是不会存储您的密码原文的，而是存储的密码的HASH摘要，在密码校验时与客户端发来的密码摘要进行比对（中间会有加盐操作）。故当您改变了密码算法策略时，数据库也是无法还原您的密码，再生成新的HASH算法的摘要值的。必须您手动修改一次密码或者创建一个新用户，这时新的密码将会采用您设置的HASH算法进行摘要存储，用于下次连接认证。

-   已获取GaussDB\(DWS\) 集群的公网访问地址，含IP地址和端口。具体请参见[获取集群连接地址](获取集群连接地址.md)。
-   已安装PyGreSQL第三方库。

    下载地址：[http://www.pygresql.org/download/index.html](http://www.pygresql.org/download/index.html)。

-   安装部署操作请参见：[http://www.pygresql.org/contents/install.html](http://www.pygresql.org/contents/install.html)。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   CentOS、Redhat等操作系统中使用yum命令安装，命令为：
    >    ```
    >    yum install PyGreSQL
    >    ```
    >-   PyGreSQL的使用依赖于PostgreSQL的libpq动态库（32位的PyGreSQL对应32位的libpq，64位的PyGreSQL对应64位的libpq），Linux中可以依赖yum命令解决。在Windows系统使用PyGreSQL需要先安装libpq，主要方式有两种：
    >    -   安装PostgreSQL，并配置libpq、ssl、crypto动态库位置到环境变量PATH中。
    >    -   安装psqlodbc，使用PostgreSQL ODBC驱动携带的libpq、ssl、crypto动态库。


## 使用约束<a name="section346571443710"></a>

由于PyGreSQL是基于PostgreSQL的客户端接口，它的功能GaussDB\(DWS\)并不能完全支持。具体支持情况请见下[表](#table12568181118545)。

>![](public_sys-resources/icon-note.gif) **说明：** 
>以下接口支持情况是基于Python 3.8.5及PyGreSQL 5.2.4版本。

**表 1**  DWS对PyGreSQL主要接口支持情况

<a name="table12568181118545"></a>
<table><thead align="left"><tr id="row1880714111545"><th class="cellrowborder" colspan="2" valign="top" id="mcps1.2.5.1.1"><p id="p48071211155418"><a name="p48071211155418"></a><a name="p48071211155418"></a>PyGreSQL</p>
</th>
<th class="cellrowborder" valign="top" id="mcps1.2.5.1.2"><p id="p2080716112546"><a name="p2080716112546"></a><a name="p2080716112546"></a>支持</p>
</th>
<th class="cellrowborder" valign="top" id="mcps1.2.5.1.3"><p id="p13807811195419"><a name="p13807811195419"></a><a name="p13807811195419"></a>备注</p>
</th>
</tr>
</thead>
<tbody><tr id="row1980791120545"><td class="cellrowborder" rowspan="24" valign="top" width="15%" headers="mcps1.2.5.1.1 "><p id="p1980791145413"><a name="p1980791145413"></a><a name="p1980791145413"></a>Module functions and constants</p>
</td>
<td class="cellrowborder" valign="top" width="65%" headers="mcps1.2.5.1.1 "><p id="p080751118548"><a name="p080751118548"></a><a name="p080751118548"></a>connect – Open a PostgreSQL connection</p>
</td>
<td class="cellrowborder" valign="top" width="10%" headers="mcps1.2.5.1.2 "><p id="p1480751110548"><a name="p1480751110548"></a><a name="p1480751110548"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" width="10%" headers="mcps1.2.5.1.3 "><p id="p580710115542"><a name="p580710115542"></a><a name="p580710115542"></a>-</p>
</td>
</tr>
<tr id="row19807201175419"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p19808111117542"><a name="p19808111117542"></a><a name="p19808111117542"></a>get_pqlib_version – get the version of libpq</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1980831110547"><a name="p1980831110547"></a><a name="p1980831110547"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p138081011115410"><a name="p138081011115410"></a><a name="p138081011115410"></a>-</p>
</td>
</tr>
<tr id="row11808811175413"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p158087117546"><a name="p158087117546"></a><a name="p158087117546"></a>get/set_defhost – default server host [DV]</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p6808131105413"><a name="p6808131105413"></a><a name="p6808131105413"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p580881175419"><a name="p580881175419"></a><a name="p580881175419"></a>-</p>
</td>
</tr>
<tr id="row88081911135419"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p7808211185420"><a name="p7808211185420"></a><a name="p7808211185420"></a>get/set_defport – default server port [DV]</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p158081711105417"><a name="p158081711105417"></a><a name="p158081711105417"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1808131113542"><a name="p1808131113542"></a><a name="p1808131113542"></a>-</p>
</td>
</tr>
<tr id="row1380861155418"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1180841185419"><a name="p1180841185419"></a><a name="p1180841185419"></a>get/set_defopt – default connection options [DV]</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p108081111115418"><a name="p108081111115418"></a><a name="p108081111115418"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p168081911155417"><a name="p168081911155417"></a><a name="p168081911155417"></a>-</p>
</td>
</tr>
<tr id="row88081511165415"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p12808201195410"><a name="p12808201195410"></a><a name="p12808201195410"></a>get/set_defbase – default database name [DV]</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p88084118541"><a name="p88084118541"></a><a name="p88084118541"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1680861155414"><a name="p1680861155414"></a><a name="p1680861155414"></a>-</p>
</td>
</tr>
<tr id="row168087115547"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p198081711165414"><a name="p198081711165414"></a><a name="p198081711165414"></a>get/set_defuser – default database user [DV]</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p880871105415"><a name="p880871105415"></a><a name="p880871105415"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p208089112548"><a name="p208089112548"></a><a name="p208089112548"></a>-</p>
</td>
</tr>
<tr id="row1280851115546"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p2808141195416"><a name="p2808141195416"></a><a name="p2808141195416"></a>get/set_defpasswd – default database password [DV]</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p168085117546"><a name="p168085117546"></a><a name="p168085117546"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p19808511185419"><a name="p19808511185419"></a><a name="p19808511185419"></a>-</p>
</td>
</tr>
<tr id="row8808121111547"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p18082011105415"><a name="p18082011105415"></a><a name="p18082011105415"></a>escape_string – escape a string for use within SQL</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p3808111116545"><a name="p3808111116545"></a><a name="p3808111116545"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1180991175420"><a name="p1180991175420"></a><a name="p1180991175420"></a>-</p>
</td>
</tr>
<tr id="row480941185417"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p180951117549"><a name="p180951117549"></a><a name="p180951117549"></a>escape_bytea – escape binary data for use within SQL</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p178097112546"><a name="p178097112546"></a><a name="p178097112546"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p3810161165419"><a name="p3810161165419"></a><a name="p3810161165419"></a>-</p>
</td>
</tr>
<tr id="row1981031111549"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1981071155412"><a name="p1981071155412"></a><a name="p1981071155412"></a>unescape_bytea – unescape data that has been retrieved as text</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p8810161110544"><a name="p8810161110544"></a><a name="p8810161110544"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1181021115413"><a name="p1181021115413"></a><a name="p1181021115413"></a>-</p>
</td>
</tr>
<tr id="row88101411135411"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p17810111116541"><a name="p17810111116541"></a><a name="p17810111116541"></a>get/set_namedresult – conversion to named tuples</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p168106114549"><a name="p168106114549"></a><a name="p168106114549"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p16810211105416"><a name="p16810211105416"></a><a name="p16810211105416"></a>-</p>
</td>
</tr>
<tr id="row1081071114549"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p16810141119548"><a name="p16810141119548"></a><a name="p16810141119548"></a>get/set_decimal – decimal type to be used for numeric values</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p181061185413"><a name="p181061185413"></a><a name="p181061185413"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p128104111549"><a name="p128104111549"></a><a name="p128104111549"></a>-</p>
</td>
</tr>
<tr id="row158101811155411"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p181011115417"><a name="p181011115417"></a><a name="p181011115417"></a>get/set_decimal_point – decimal mark used for monetary values</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p16810611195420"><a name="p16810611195420"></a><a name="p16810611195420"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1781041155411"><a name="p1781041155411"></a><a name="p1781041155411"></a>-</p>
</td>
</tr>
<tr id="row1181015119547"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p18810201145411"><a name="p18810201145411"></a><a name="p18810201145411"></a>get/set_bool – whether boolean values are returned as bool objects</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p781031116541"><a name="p781031116541"></a><a name="p781031116541"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p16810811195416"><a name="p16810811195416"></a><a name="p16810811195416"></a>-</p>
</td>
</tr>
<tr id="row28101111135411"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p181091195415"><a name="p181091195415"></a><a name="p181091195415"></a>get/set_array – whether arrays are returned as list objects</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p4810141125419"><a name="p4810141125419"></a><a name="p4810141125419"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1681051115412"><a name="p1681051115412"></a><a name="p1681051115412"></a>-</p>
</td>
</tr>
<tr id="row3810161110542"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p13810151110548"><a name="p13810151110548"></a><a name="p13810151110548"></a>get/set_bytea_escaped – whether bytea data is returned escaped</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p10810131111546"><a name="p10810131111546"></a><a name="p10810131111546"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p198101111185413"><a name="p198101111185413"></a><a name="p198101111185413"></a>-</p>
</td>
</tr>
<tr id="row18810171112546"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p381071115546"><a name="p381071115546"></a><a name="p381071115546"></a>get/set_jsondecode – decoding JSON format</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p6810101111541"><a name="p6810101111541"></a><a name="p6810101111541"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p38101111105411"><a name="p38101111105411"></a><a name="p38101111105411"></a>-</p>
</td>
</tr>
<tr id="row148111311155418"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p481161135415"><a name="p481161135415"></a><a name="p481161135415"></a>get/set_cast_hook – fallback typecast function</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p4811211205413"><a name="p4811211205413"></a><a name="p4811211205413"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1281117114543"><a name="p1281117114543"></a><a name="p1281117114543"></a>-</p>
</td>
</tr>
<tr id="row13811111113549"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p13811121165412"><a name="p13811121165412"></a><a name="p13811121165412"></a>get/set_datestyle – assume a fixed date style</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1581181118545"><a name="p1581181118545"></a><a name="p1581181118545"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1811201125416"><a name="p1811201125416"></a><a name="p1811201125416"></a>-</p>
</td>
</tr>
<tr id="row1281121175414"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p19811111112546"><a name="p19811111112546"></a><a name="p19811111112546"></a>get/set_typecast – custom typecasting</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p178111411105412"><a name="p178111411105412"></a><a name="p178111411105412"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p58111511135412"><a name="p58111511135412"></a><a name="p58111511135412"></a>-</p>
</td>
</tr>
<tr id="row19811151118545"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p981131195416"><a name="p981131195416"></a><a name="p981131195416"></a>cast_array/record – fast parsers for arrays and records</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p2811101165417"><a name="p2811101165417"></a><a name="p2811101165417"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p28113118544"><a name="p28113118544"></a><a name="p28113118544"></a>-</p>
</td>
</tr>
<tr id="row7811121105414"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1481101110548"><a name="p1481101110548"></a><a name="p1481101110548"></a>Type helpers</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p68111911195413"><a name="p68111911195413"></a><a name="p68111911195413"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p3811141195417"><a name="p3811141195417"></a><a name="p3811141195417"></a>-</p>
</td>
</tr>
<tr id="row3811151195412"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p18118111542"><a name="p18118111542"></a><a name="p18118111542"></a>Module constants</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1681131110549"><a name="p1681131110549"></a><a name="p1681131110549"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p7811111135411"><a name="p7811111135411"></a><a name="p7811111135411"></a>-</p>
</td>
</tr>
<tr id="row12811181119547"><td class="cellrowborder" rowspan="25" valign="top" width="15%" headers="mcps1.2.5.1.1 "><p id="p1081112117547"><a name="p1081112117547"></a><a name="p1081112117547"></a>Connection – The connection object</p>
</td>
<td class="cellrowborder" valign="top" width="65%" headers="mcps1.2.5.1.1 "><p id="p178111911115418"><a name="p178111911115418"></a><a name="p178111911115418"></a>query – execute a SQL command string</p>
</td>
<td class="cellrowborder" valign="top" width="10%" headers="mcps1.2.5.1.2 "><p id="p198118119541"><a name="p198118119541"></a><a name="p198118119541"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" width="10%" headers="mcps1.2.5.1.3 "><p id="p1181115119547"><a name="p1181115119547"></a><a name="p1181115119547"></a>-</p>
</td>
</tr>
<tr id="row081101125412"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p2081116116548"><a name="p2081116116548"></a><a name="p2081116116548"></a>send_query - executes a SQL command string asynchronously</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p8811511175412"><a name="p8811511175412"></a><a name="p8811511175412"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1381171120548"><a name="p1381171120548"></a><a name="p1381171120548"></a>-</p>
</td>
</tr>
<tr id="row148121011155412"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1881261112546"><a name="p1881261112546"></a><a name="p1881261112546"></a>query_prepared – execute a prepared statement</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p198120115548"><a name="p198120115548"></a><a name="p198120115548"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p18123114546"><a name="p18123114546"></a><a name="p18123114546"></a>-</p>
</td>
</tr>
<tr id="row11812101114546"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p48121411155417"><a name="p48121411155417"></a><a name="p48121411155417"></a>prepare – create a prepared statement</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p4812111115411"><a name="p4812111115411"></a><a name="p4812111115411"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p5812101185415"><a name="p5812101185415"></a><a name="p5812101185415"></a>-</p>
</td>
</tr>
<tr id="row1481218113548"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p2812171114547"><a name="p2812171114547"></a><a name="p2812171114547"></a>describe_prepared – describe a prepared statement</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p17812191175417"><a name="p17812191175417"></a><a name="p17812191175417"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p98122114546"><a name="p98122114546"></a><a name="p98122114546"></a>-</p>
</td>
</tr>
<tr id="row1781291135415"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p13812511135412"><a name="p13812511135412"></a><a name="p13812511135412"></a>reset – reset the connection</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p118121311165411"><a name="p118121311165411"></a><a name="p118121311165411"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p16812711175414"><a name="p16812711175414"></a><a name="p16812711175414"></a>-</p>
</td>
</tr>
<tr id="row281261175413"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p15812141185411"><a name="p15812141185411"></a><a name="p15812141185411"></a>poll - completes an asynchronous connection</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p781210113548"><a name="p781210113548"></a><a name="p781210113548"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1781201165413"><a name="p1781201165413"></a><a name="p1781201165413"></a>-</p>
</td>
</tr>
<tr id="row681271112549"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p281217114548"><a name="p281217114548"></a><a name="p281217114548"></a>cancel – abandon processing of current SQL command</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p5812101135411"><a name="p5812101135411"></a><a name="p5812101135411"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p3812191112540"><a name="p3812191112540"></a><a name="p3812191112540"></a>-</p>
</td>
</tr>
<tr id="row19812191135413"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p12812191119542"><a name="p12812191119542"></a><a name="p12812191119542"></a>close – close the database connection</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1781291112542"><a name="p1781291112542"></a><a name="p1781291112542"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1481210115549"><a name="p1481210115549"></a><a name="p1481210115549"></a>-</p>
</td>
</tr>
<tr id="row08121111175416"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1081214117549"><a name="p1081214117549"></a><a name="p1081214117549"></a>transaction – get the current transaction state</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1081217116543"><a name="p1081217116543"></a><a name="p1081217116543"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p081216113545"><a name="p081216113545"></a><a name="p081216113545"></a>-</p>
</td>
</tr>
<tr id="row3812161145414"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p5813411125417"><a name="p5813411125417"></a><a name="p5813411125417"></a>parameter – get a current server parameter setting</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p88137119548"><a name="p88137119548"></a><a name="p88137119548"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1813011145416"><a name="p1813011145416"></a><a name="p1813011145416"></a>-</p>
</td>
</tr>
<tr id="row1181351115417"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p2813201155416"><a name="p2813201155416"></a><a name="p2813201155416"></a>date_format – get the currently used date format</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1781321112547"><a name="p1781321112547"></a><a name="p1781321112547"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1813171111547"><a name="p1813171111547"></a><a name="p1813171111547"></a>-</p>
</td>
</tr>
<tr id="row17813101155411"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p981310115543"><a name="p981310115543"></a><a name="p981310115543"></a>fileno – get the socket used to connect to the database</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1781381113548"><a name="p1781381113548"></a><a name="p1781381113548"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1681361175414"><a name="p1681361175414"></a><a name="p1681361175414"></a>-</p>
</td>
</tr>
<tr id="row1081391135413"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p38131211115410"><a name="p38131211115410"></a><a name="p38131211115410"></a>set_non_blocking - set the non-blocking status of the connection</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p481381120540"><a name="p481381120540"></a><a name="p481381120540"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1881381125418"><a name="p1881381125418"></a><a name="p1881381125418"></a>-</p>
</td>
</tr>
<tr id="row118131611165414"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1881341115410"><a name="p1881341115410"></a><a name="p1881341115410"></a>is_non_blocking - report the blocking status of the connection</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p2081319119547"><a name="p2081319119547"></a><a name="p2081319119547"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p281311115543"><a name="p281311115543"></a><a name="p281311115543"></a>-</p>
</td>
</tr>
<tr id="row18131711125420"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p481321185411"><a name="p481321185411"></a><a name="p481321185411"></a>getnotify – get the last notify from the server</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p78131115542"><a name="p78131115542"></a><a name="p78131115542"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1181314115549"><a name="p1181314115549"></a><a name="p1181314115549"></a>数据库不支持listen/notify</p>
</td>
</tr>
<tr id="row1181321105412"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p188131511115414"><a name="p188131511115414"></a><a name="p188131511115414"></a>inserttable – insert a list into a table</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p4813141111541"><a name="p4813141111541"></a><a name="p4813141111541"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1381341115411"><a name="p1381341115411"></a><a name="p1381341115411"></a>copy命令中如果有\n，请使用双引号引用此字段</p>
</td>
</tr>
<tr id="row481341111549"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p20813111117548"><a name="p20813111117548"></a><a name="p20813111117548"></a>get/set_notice_receiver – custom notice receiver</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p4813171111549"><a name="p4813171111549"></a><a name="p4813171111549"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1881371118545"><a name="p1881371118545"></a><a name="p1881371118545"></a>-</p>
</td>
</tr>
<tr id="row28132112545"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p98139112542"><a name="p98139112542"></a><a name="p98139112542"></a>putline – write a line to the server socket [DA]</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p188147117546"><a name="p188147117546"></a><a name="p188147117546"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1281411119544"><a name="p1281411119544"></a><a name="p1281411119544"></a>-</p>
</td>
</tr>
<tr id="row18141511115416"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p5814141155416"><a name="p5814141155416"></a><a name="p5814141155416"></a>getline – get a line from server socket [DA]</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p17814131145418"><a name="p17814131145418"></a><a name="p17814131145418"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p13814111112549"><a name="p13814111112549"></a><a name="p13814111112549"></a>-</p>
</td>
</tr>
<tr id="row13814161113549"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p16814911125416"><a name="p16814911125416"></a><a name="p16814911125416"></a>endcopy – synchronize client and server [DA]</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p148141211135414"><a name="p148141211135414"></a><a name="p148141211135414"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p18142011105419"><a name="p18142011105419"></a><a name="p18142011105419"></a>-</p>
</td>
</tr>
<tr id="row19814161114548"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p88143119546"><a name="p88143119546"></a><a name="p88143119546"></a>locreate – create a large object in the database [LO]</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p281421113545"><a name="p281421113545"></a><a name="p281421113545"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p5814121155417"><a name="p5814121155417"></a><a name="p5814121155417"></a>大对象相关操作</p>
</td>
</tr>
<tr id="row58142119543"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1814171114543"><a name="p1814171114543"></a><a name="p1814171114543"></a>getlo – build a large object from given oid [LO]</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p081411119542"><a name="p081411119542"></a><a name="p081411119542"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p10814111115542"><a name="p10814111115542"></a><a name="p10814111115542"></a>大对象相关操作</p>
</td>
</tr>
<tr id="row19814131114540"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p281401175411"><a name="p281401175411"></a><a name="p281401175411"></a>loimport – import a file to a large object [LO]</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p48141911195410"><a name="p48141911195410"></a><a name="p48141911195410"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p681481112540"><a name="p681481112540"></a><a name="p681481112540"></a>大对象相关操作</p>
</td>
</tr>
<tr id="row9814121125418"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p17814121119541"><a name="p17814121119541"></a><a name="p17814121119541"></a>Object attributes</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p15814121175417"><a name="p15814121175417"></a><a name="p15814121175417"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p981411125417"><a name="p981411125417"></a><a name="p981411125417"></a>-</p>
</td>
</tr>
<tr id="row7814121185417"><td class="cellrowborder" rowspan="29" valign="top" width="15%" headers="mcps1.2.5.1.1 "><p id="p198146114547"><a name="p198146114547"></a><a name="p198146114547"></a>The DB wrapper class</p>
</td>
<td class="cellrowborder" valign="top" width="65%" headers="mcps1.2.5.1.1 "><p id="p4814191195419"><a name="p4814191195419"></a><a name="p4814191195419"></a>Initialization</p>
</td>
<td class="cellrowborder" valign="top" width="10%" headers="mcps1.2.5.1.2 "><p id="p118141311115411"><a name="p118141311115411"></a><a name="p118141311115411"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" width="10%" headers="mcps1.2.5.1.3 "><p id="p5814911175412"><a name="p5814911175412"></a><a name="p5814911175412"></a>-</p>
</td>
</tr>
<tr id="row1381420114548"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p681401145420"><a name="p681401145420"></a><a name="p681401145420"></a>pkey – return the primary key of a table</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1281515115548"><a name="p1281515115548"></a><a name="p1281515115548"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p15815111114547"><a name="p15815111114547"></a><a name="p15815111114547"></a>-</p>
</td>
</tr>
<tr id="row8815191165413"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p13815211125419"><a name="p13815211125419"></a><a name="p13815211125419"></a>get_databases – get list of databases in the system</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p13815141115410"><a name="p13815141115410"></a><a name="p13815141115410"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p13815111111546"><a name="p13815111111546"></a><a name="p13815111111546"></a>-</p>
</td>
</tr>
<tr id="row17815211125416"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1181516112541"><a name="p1181516112541"></a><a name="p1181516112541"></a>get_relations – get list of relations in connected database</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p118150115549"><a name="p118150115549"></a><a name="p118150115549"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p148151211105412"><a name="p148151211105412"></a><a name="p148151211105412"></a>-</p>
</td>
</tr>
<tr id="row1781581185418"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p181501125417"><a name="p181501125417"></a><a name="p181501125417"></a>get_tables – get list of tables in connected database</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p18815141112543"><a name="p18815141112543"></a><a name="p18815141112543"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p281519113544"><a name="p281519113544"></a><a name="p281519113544"></a>-</p>
</td>
</tr>
<tr id="row128151311175411"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p128155114541"><a name="p128155114541"></a><a name="p128155114541"></a>get_attnames – get the attribute names of a table</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p48157116544"><a name="p48157116544"></a><a name="p48157116544"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p10815111105410"><a name="p10815111105410"></a><a name="p10815111105410"></a>-</p>
</td>
</tr>
<tr id="row168151911155415"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p10815211185410"><a name="p10815211185410"></a><a name="p10815211185410"></a>has_table_privilege – check table privilege</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p481561113542"><a name="p481561113542"></a><a name="p481561113542"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p148155119547"><a name="p148155119547"></a><a name="p148155119547"></a>-</p>
</td>
</tr>
<tr id="row198151211165415"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p178151114544"><a name="p178151114544"></a><a name="p178151114544"></a>get/set_parameter – get or set run-time parameters</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p781671112549"><a name="p781671112549"></a><a name="p781671112549"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p10816811135417"><a name="p10816811135417"></a><a name="p10816811135417"></a>-</p>
</td>
</tr>
<tr id="row3816511205414"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1816151155412"><a name="p1816151155412"></a><a name="p1816151155412"></a>begin/commit/rollback/savepoint/release – transaction handling</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1081611113540"><a name="p1081611113540"></a><a name="p1081611113540"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p10816411165417"><a name="p10816411165417"></a><a name="p10816411165417"></a>-</p>
</td>
</tr>
<tr id="row20816171110546"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p4816811135410"><a name="p4816811135410"></a><a name="p4816811135410"></a>get – get a row from a database table or view</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p11816111115541"><a name="p11816111115541"></a><a name="p11816111115541"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p481611119548"><a name="p481611119548"></a><a name="p481611119548"></a>-</p>
</td>
</tr>
<tr id="row158161311105417"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1881741112543"><a name="p1881741112543"></a><a name="p1881741112543"></a>insert – insert a row into a database table</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1381713111545"><a name="p1381713111545"></a><a name="p1381713111545"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p16817111175416"><a name="p16817111175416"></a><a name="p16817111175416"></a>-</p>
</td>
</tr>
<tr id="row481721115543"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1981781110543"><a name="p1981781110543"></a><a name="p1981781110543"></a>update – update a row in a database table</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p168175114541"><a name="p168175114541"></a><a name="p168175114541"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p9817171125419"><a name="p9817171125419"></a><a name="p9817171125419"></a>-</p>
</td>
</tr>
<tr id="row178174116549"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p98171811145414"><a name="p98171811145414"></a><a name="p98171811145414"></a>upsert – insert a row with conflict resolution</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p981761145412"><a name="p981761145412"></a><a name="p981761145412"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p118171711165419"><a name="p118171711165419"></a><a name="p118171711165419"></a>-</p>
</td>
</tr>
<tr id="row4817131113542"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p17817111155417"><a name="p17817111155417"></a><a name="p17817111155417"></a>query – execute a SQL command string</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1181721165415"><a name="p1181721165415"></a><a name="p1181721165415"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p128171611135414"><a name="p128171611135414"></a><a name="p128171611135414"></a>-</p>
</td>
</tr>
<tr id="row148171911135418"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p15817131165418"><a name="p15817131165418"></a><a name="p15817131165418"></a>query_formatted – execute a formatted SQL command string</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p3817811125416"><a name="p3817811125416"></a><a name="p3817811125416"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p88171011105416"><a name="p88171011105416"></a><a name="p88171011105416"></a>-</p>
</td>
</tr>
<tr id="row8817141112548"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1581721185414"><a name="p1581721185414"></a><a name="p1581721185414"></a>query_prepared – execute a prepared statement</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p381721105412"><a name="p381721105412"></a><a name="p381721105412"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p19817171155413"><a name="p19817171155413"></a><a name="p19817171155413"></a>-</p>
</td>
</tr>
<tr id="row4817101111541"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p68171511205410"><a name="p68171511205410"></a><a name="p68171511205410"></a>prepare – create a prepared statement</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p17817611145414"><a name="p17817611145414"></a><a name="p17817611145414"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p6817121116543"><a name="p6817121116543"></a><a name="p6817121116543"></a>-</p>
</td>
</tr>
<tr id="row17817211175412"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p181716115549"><a name="p181716115549"></a><a name="p181716115549"></a>describe_prepared – describe a prepared statement</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p481731165411"><a name="p481731165411"></a><a name="p481731165411"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p10817161125413"><a name="p10817161125413"></a><a name="p10817161125413"></a>-</p>
</td>
</tr>
<tr id="row14817191135411"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p981751116548"><a name="p981751116548"></a><a name="p981751116548"></a>delete_prepared – delete a prepared statement</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1081814119546"><a name="p1081814119546"></a><a name="p1081814119546"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p2818911175413"><a name="p2818911175413"></a><a name="p2818911175413"></a>-</p>
</td>
</tr>
<tr id="row148181011135410"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p881813117543"><a name="p881813117543"></a><a name="p881813117543"></a>clear – clear row values in memory</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p148189117548"><a name="p148189117548"></a><a name="p148189117548"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p2818181175416"><a name="p2818181175416"></a><a name="p2818181175416"></a>-</p>
</td>
</tr>
<tr id="row148181114545"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p11818141175412"><a name="p11818141175412"></a><a name="p11818141175412"></a>delete – delete a row from a database table</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p3818111105410"><a name="p3818111105410"></a><a name="p3818111105410"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p28181611155419"><a name="p28181611155419"></a><a name="p28181611155419"></a>元组必须有唯一键或者主键</p>
</td>
</tr>
<tr id="row1081810118541"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p4818131175414"><a name="p4818131175414"></a><a name="p4818131175414"></a>truncate – quickly empty database tables</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p13818191116546"><a name="p13818191116546"></a><a name="p13818191116546"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p38181111175412"><a name="p38181111175412"></a><a name="p38181111175412"></a>-</p>
</td>
</tr>
<tr id="row11818121195415"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1681851117541"><a name="p1681851117541"></a><a name="p1681851117541"></a>get_as_list/dict – read a table as a list or dictionary</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p198184119547"><a name="p198184119547"></a><a name="p198184119547"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1481811111546"><a name="p1481811111546"></a><a name="p1481811111546"></a>-</p>
</td>
</tr>
<tr id="row1081881118548"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p28183118544"><a name="p28183118544"></a><a name="p28183118544"></a>escape_literal/identifier/string/bytea – escape for SQL</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p6818181119546"><a name="p6818181119546"></a><a name="p6818181119546"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p681841110541"><a name="p681841110541"></a><a name="p681841110541"></a>-</p>
</td>
</tr>
<tr id="row1981861114541"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p168181711205411"><a name="p168181711205411"></a><a name="p168181711205411"></a>unescape_bytea – unescape data retrieved from the database</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p14818161155418"><a name="p14818161155418"></a><a name="p14818161155418"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p3818131105414"><a name="p3818131105414"></a><a name="p3818131105414"></a>-</p>
</td>
</tr>
<tr id="row17818131115544"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1981820111545"><a name="p1981820111545"></a><a name="p1981820111545"></a>encode/decode_json – encode and decode JSON data</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1581871135415"><a name="p1581871135415"></a><a name="p1581871135415"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p168181115542"><a name="p168181115542"></a><a name="p168181115542"></a>-</p>
</td>
</tr>
<tr id="row1381851135413"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p981831155413"><a name="p981831155413"></a><a name="p981831155413"></a>use_regtypes – determine use of regular type names</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p08191711185419"><a name="p08191711185419"></a><a name="p08191711185419"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p158191611155412"><a name="p158191611155412"></a><a name="p158191611155412"></a>-</p>
</td>
</tr>
<tr id="row9819181115547"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p98191211165414"><a name="p98191211165414"></a><a name="p98191211165414"></a>notification_handler – create a notification handler</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p581921119549"><a name="p581921119549"></a><a name="p581921119549"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p11819151175416"><a name="p11819151175416"></a><a name="p11819151175416"></a>数据库不支持listen/notify</p>
</td>
</tr>
<tr id="row481913119540"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1881918115541"><a name="p1881918115541"></a><a name="p1881918115541"></a>Attributes of the DB wrapper class</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p8819611165419"><a name="p8819611165419"></a><a name="p8819611165419"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p138191411135413"><a name="p138191411135413"></a><a name="p138191411135413"></a>-</p>
</td>
</tr>
<tr id="row15819711105419"><td class="cellrowborder" rowspan="11" valign="top" width="15%" headers="mcps1.2.5.1.1 "><p id="p19819511145413"><a name="p19819511145413"></a><a name="p19819511145413"></a>Query methods</p>
</td>
<td class="cellrowborder" valign="top" width="65%" headers="mcps1.2.5.1.1 "><p id="p881961195415"><a name="p881961195415"></a><a name="p881961195415"></a>getresult – get query values as list of tuples</p>
</td>
<td class="cellrowborder" valign="top" width="10%" headers="mcps1.2.5.1.2 "><p id="p1181913112545"><a name="p1181913112545"></a><a name="p1181913112545"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" width="10%" headers="mcps1.2.5.1.3 "><p id="p13819151185418"><a name="p13819151185418"></a><a name="p13819151185418"></a>-</p>
</td>
</tr>
<tr id="row1681961165410"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p781931175410"><a name="p781931175410"></a><a name="p781931175410"></a>dictresult/dictiter – get query values as dictionaries</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p881951120546"><a name="p881951120546"></a><a name="p881951120546"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p581914116548"><a name="p581914116548"></a><a name="p581914116548"></a>-</p>
</td>
</tr>
<tr id="row98191411115418"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1481911118544"><a name="p1481911118544"></a><a name="p1481911118544"></a>namedresult/namediter – get query values as named tuples</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p6819131115546"><a name="p6819131115546"></a><a name="p6819131115546"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p188191116547"><a name="p188191116547"></a><a name="p188191116547"></a>-</p>
</td>
</tr>
<tr id="row1381951145411"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p128198115543"><a name="p128198115543"></a><a name="p128198115543"></a>scalarresult/scalariter – get query values as scalars</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1281971185417"><a name="p1281971185417"></a><a name="p1281971185417"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p188192116547"><a name="p188192116547"></a><a name="p188192116547"></a>-</p>
</td>
</tr>
<tr id="row58196114541"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p148198118543"><a name="p148198118543"></a><a name="p148198118543"></a>one/onedict/onenamed/onescalar – get one result of a query</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1981971115410"><a name="p1981971115410"></a><a name="p1981971115410"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p681981135416"><a name="p681981135416"></a><a name="p681981135416"></a>-</p>
</td>
</tr>
<tr id="row108198118547"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1381910115546"><a name="p1381910115546"></a><a name="p1381910115546"></a>single/singledict/singlenamed/singlescalar – get single result of a query</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p18819121165420"><a name="p18819121165420"></a><a name="p18819121165420"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p15820131113546"><a name="p15820131113546"></a><a name="p15820131113546"></a>-</p>
</td>
</tr>
<tr id="row198201811175416"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p11820121118544"><a name="p11820121118544"></a><a name="p11820121118544"></a>listfields – list fields names of previous query result</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p158202011195413"><a name="p158202011195413"></a><a name="p158202011195413"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p4820111165417"><a name="p4820111165417"></a><a name="p4820111165417"></a>-</p>
</td>
</tr>
<tr id="row128201611145419"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p12820171195412"><a name="p12820171195412"></a><a name="p12820171195412"></a>fieldname, fieldnum – field name/number conversion</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p782071115413"><a name="p782071115413"></a><a name="p782071115413"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p16820181110548"><a name="p16820181110548"></a><a name="p16820181110548"></a>-</p>
</td>
</tr>
<tr id="row188201511195417"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p17820141111545"><a name="p17820141111545"></a><a name="p17820141111545"></a>fieldinfo – detailed info about query result fields</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1582018115544"><a name="p1582018115544"></a><a name="p1582018115544"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p5820411195418"><a name="p5820411195418"></a><a name="p5820411195418"></a>-</p>
</td>
</tr>
<tr id="row18820191115418"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1082061113545"><a name="p1082061113545"></a><a name="p1082061113545"></a>ntuples – return number of tuples in query object</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p48209110546"><a name="p48209110546"></a><a name="p48209110546"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p482012110546"><a name="p482012110546"></a><a name="p482012110546"></a>-</p>
</td>
</tr>
<tr id="row28204115545"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p12820141117549"><a name="p12820141117549"></a><a name="p12820141117549"></a>memsize – return number of bytes allocated by query result</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p16820151115546"><a name="p16820151115546"></a><a name="p16820151115546"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p16820611115416"><a name="p16820611115416"></a><a name="p16820611115416"></a>-</p>
</td>
</tr>
<tr id="row1820191115415"><td class="cellrowborder" rowspan="6" valign="top" width="15%" headers="mcps1.2.5.1.1 "><p id="p48207115546"><a name="p48207115546"></a><a name="p48207115546"></a>LargeObject – Large Objects</p>
</td>
<td class="cellrowborder" valign="top" width="65%" headers="mcps1.2.5.1.1 "><p id="p1982012119543"><a name="p1982012119543"></a><a name="p1982012119543"></a>open – open a large object</p>
</td>
<td class="cellrowborder" valign="top" width="10%" headers="mcps1.2.5.1.2 "><p id="p19820151165416"><a name="p19820151165416"></a><a name="p19820151165416"></a>N</p>
</td>
<td class="cellrowborder" valign="top" width="10%" headers="mcps1.2.5.1.3 "><p id="p582015115548"><a name="p582015115548"></a><a name="p582015115548"></a>大对象相关操作</p>
</td>
</tr>
<tr id="row16820181125417"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1382013114542"><a name="p1382013114542"></a><a name="p1382013114542"></a>close – close a large object</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p10820211105414"><a name="p10820211105414"></a><a name="p10820211105414"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1820511205419"><a name="p1820511205419"></a><a name="p1820511205419"></a>大对象相关操作</p>
</td>
</tr>
<tr id="row38201411125411"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p8820201120548"><a name="p8820201120548"></a><a name="p8820201120548"></a>read, write, tell, seek, unlink – file-like large object handling</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p882071145417"><a name="p882071145417"></a><a name="p882071145417"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p9821191145419"><a name="p9821191145419"></a><a name="p9821191145419"></a>大对象相关操作</p>
</td>
</tr>
<tr id="row1482141165410"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1382151135416"><a name="p1382151135416"></a><a name="p1382151135416"></a>size – get the large object size</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p18211111165412"><a name="p18211111165412"></a><a name="p18211111165412"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p6821211105412"><a name="p6821211105412"></a><a name="p6821211105412"></a>大对象相关操作</p>
</td>
</tr>
<tr id="row158211911125415"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p188211511105420"><a name="p188211511105420"></a><a name="p188211511105420"></a>export – save a large object to a file</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1582116113544"><a name="p1582116113544"></a><a name="p1582116113544"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1482117113542"><a name="p1482117113542"></a><a name="p1482117113542"></a>大对象相关操作</p>
</td>
</tr>
<tr id="row68211911135415"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p15821161111542"><a name="p15821161111542"></a><a name="p15821161111542"></a>Object attributes</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p6821101155420"><a name="p6821101155420"></a><a name="p6821101155420"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p3821131195416"><a name="p3821131195416"></a><a name="p3821131195416"></a>大对象相关操作</p>
</td>
</tr>
<tr id="row782118112543"><td class="cellrowborder" rowspan="4" valign="top" width="15%" headers="mcps1.2.5.1.1 "><p id="p88210117549"><a name="p88210117549"></a><a name="p88210117549"></a>The Notification Handler</p>
</td>
<td class="cellrowborder" valign="top" width="65%" headers="mcps1.2.5.1.1 "><p id="p1082161135413"><a name="p1082161135413"></a><a name="p1082161135413"></a>Instantiating the notification handler</p>
</td>
<td class="cellrowborder" valign="top" width="10%" headers="mcps1.2.5.1.2 "><p id="p14821111145411"><a name="p14821111145411"></a><a name="p14821111145411"></a>N</p>
</td>
<td class="cellrowborder" valign="top" width="10%" headers="mcps1.2.5.1.3 "><p id="p18821191111543"><a name="p18821191111543"></a><a name="p18821191111543"></a>数据库不支持listen/notify</p>
</td>
</tr>
<tr id="row178211011105415"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1782191113541"><a name="p1782191113541"></a><a name="p1782191113541"></a>Invoking the notification handler</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p15821911115416"><a name="p15821911115416"></a><a name="p15821911115416"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p2082101135417"><a name="p2082101135417"></a><a name="p2082101135417"></a>数据库不支持listen/notify</p>
</td>
</tr>
<tr id="row0822311165415"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p98227115547"><a name="p98227115547"></a><a name="p98227115547"></a>Sending notifications</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p10822611185414"><a name="p10822611185414"></a><a name="p10822611185414"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p20822161195414"><a name="p20822161195414"></a><a name="p20822161195414"></a>数据库不支持listen/notify</p>
</td>
</tr>
<tr id="row682271155419"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p18822911125412"><a name="p18822911125412"></a><a name="p18822911125412"></a>Auxiliary methods</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p88227117543"><a name="p88227117543"></a><a name="p88227117543"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p18822911185415"><a name="p18822911185415"></a><a name="p18822911185415"></a>数据库不支持listen/notify</p>
</td>
</tr>
<tr id="row982261110542"><td class="cellrowborder" colspan="4" valign="top" headers="mcps1.2.5.1.1 mcps1.2.5.1.2 mcps1.2.5.1.3 "><p id="p17822711195417"><a name="p17822711195417"></a><a name="p17822711195417"></a><strong id="b1182241125413"><a name="b1182241125413"></a><a name="b1182241125413"></a>pgdb</strong></p>
</td>
</tr>
<tr id="row19822111110548"><td class="cellrowborder" rowspan="4" valign="top" width="15%" headers="mcps1.2.5.1.1 "><p id="p4822111113541"><a name="p4822111113541"></a><a name="p4822111113541"></a>Module functions and constants</p>
</td>
<td class="cellrowborder" valign="top" width="65%" headers="mcps1.2.5.1.1 "><p id="p1822151119542"><a name="p1822151119542"></a><a name="p1822151119542"></a>connect – Open a PostgreSQL connection</p>
</td>
<td class="cellrowborder" valign="top" width="10%" headers="mcps1.2.5.1.2 "><p id="p182281118545"><a name="p182281118545"></a><a name="p182281118545"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" width="10%" headers="mcps1.2.5.1.3 "><p id="p682211117549"><a name="p682211117549"></a><a name="p682211117549"></a>-</p>
</td>
</tr>
<tr id="row11822121113542"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p198231911125419"><a name="p198231911125419"></a><a name="p198231911125419"></a>get/set/reset_typecast – Control the global typecast functions</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p13823111105418"><a name="p13823111105418"></a><a name="p13823111105418"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p208231611165414"><a name="p208231611165414"></a><a name="p208231611165414"></a>-</p>
</td>
</tr>
<tr id="row2823111117543"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p082315115545"><a name="p082315115545"></a><a name="p082315115545"></a>Module constants</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p8823171120546"><a name="p8823171120546"></a><a name="p8823171120546"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1282311111545"><a name="p1282311111545"></a><a name="p1282311111545"></a>-</p>
</td>
</tr>
<tr id="row3823211185412"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p148236114547"><a name="p148236114547"></a><a name="p148236114547"></a>Errors raised by this module</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1182331118545"><a name="p1182331118545"></a><a name="p1182331118545"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p782391111542"><a name="p782391111542"></a><a name="p782391111542"></a>-</p>
</td>
</tr>
<tr id="row17823121116548"><td class="cellrowborder" rowspan="5" valign="top" width="15%" headers="mcps1.2.5.1.1 "><p id="p1823181116549"><a name="p1823181116549"></a><a name="p1823181116549"></a>Connection – The connection object</p>
</td>
<td class="cellrowborder" valign="top" width="65%" headers="mcps1.2.5.1.1 "><p id="p5823181118549"><a name="p5823181118549"></a><a name="p5823181118549"></a>close – close the connection</p>
</td>
<td class="cellrowborder" valign="top" width="10%" headers="mcps1.2.5.1.2 "><p id="p1382331175416"><a name="p1382331175416"></a><a name="p1382331175416"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" width="10%" headers="mcps1.2.5.1.3 "><p id="p582361110543"><a name="p582361110543"></a><a name="p582361110543"></a>-</p>
</td>
</tr>
<tr id="row15823161110543"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p48236111540"><a name="p48236111540"></a><a name="p48236111540"></a>commit – commit the connection</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p11823171165415"><a name="p11823171165415"></a><a name="p11823171165415"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p98231411115417"><a name="p98231411115417"></a><a name="p98231411115417"></a>-</p>
</td>
</tr>
<tr id="row48237118545"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p118237112542"><a name="p118237112542"></a><a name="p118237112542"></a>rollback – roll back the connection</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p38231111175417"><a name="p38231111175417"></a><a name="p38231111175417"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p282391105414"><a name="p282391105414"></a><a name="p282391105414"></a>-</p>
</td>
</tr>
<tr id="row1682311195416"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p882301115541"><a name="p882301115541"></a><a name="p882301115541"></a>cursor – return a new cursor object</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p18823311155419"><a name="p18823311155419"></a><a name="p18823311155419"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p188238115542"><a name="p188238115542"></a><a name="p188238115542"></a>-</p>
</td>
</tr>
<tr id="row12823171118540"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p98231115549"><a name="p98231115549"></a><a name="p98231115549"></a>Attributes that are not part of the standard</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p18823181114544"><a name="p18823181114544"></a><a name="p18823181114544"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p982441115419"><a name="p982441115419"></a><a name="p982441115419"></a>-</p>
</td>
</tr>
<tr id="row382411114543"><td class="cellrowborder" rowspan="11" valign="top" width="15%" headers="mcps1.2.5.1.1 "><p id="p18241911185410"><a name="p18241911185410"></a><a name="p18241911185410"></a>Cursor – The cursor object</p>
</td>
<td class="cellrowborder" valign="top" width="65%" headers="mcps1.2.5.1.1 "><p id="p782441114544"><a name="p782441114544"></a><a name="p782441114544"></a>description – details regarding the result columns</p>
</td>
<td class="cellrowborder" valign="top" width="10%" headers="mcps1.2.5.1.2 "><p id="p11824911115415"><a name="p11824911115415"></a><a name="p11824911115415"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" width="10%" headers="mcps1.2.5.1.3 "><p id="p1782419112543"><a name="p1782419112543"></a><a name="p1782419112543"></a>-</p>
</td>
</tr>
<tr id="row128247110546"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p8824201115545"><a name="p8824201115545"></a><a name="p8824201115545"></a>rowcount – number of rows of the result</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p17824181120549"><a name="p17824181120549"></a><a name="p17824181120549"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1824011105411"><a name="p1824011105411"></a><a name="p1824011105411"></a>-</p>
</td>
</tr>
<tr id="row13824411125411"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p14824811205415"><a name="p14824811205415"></a><a name="p14824811205415"></a>close – close the cursor</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p6824161125413"><a name="p6824161125413"></a><a name="p6824161125413"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1182431114547"><a name="p1182431114547"></a><a name="p1182431114547"></a>-</p>
</td>
</tr>
<tr id="row148246118540"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p108241311175412"><a name="p108241311175412"></a><a name="p108241311175412"></a>execute – execute a database operation</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p582418118545"><a name="p582418118545"></a><a name="p582418118545"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p6824911155418"><a name="p6824911155418"></a><a name="p6824911155418"></a>-</p>
</td>
</tr>
<tr id="row14824191115541"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p382415119546"><a name="p382415119546"></a><a name="p382415119546"></a>executemany – execute many similar database operations</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p28243118547"><a name="p28243118547"></a><a name="p28243118547"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p5824011175417"><a name="p5824011175417"></a><a name="p5824011175417"></a>-</p>
</td>
</tr>
<tr id="row28241911205413"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p6824171175415"><a name="p6824171175415"></a><a name="p6824171175415"></a>callproc – Call a stored procedure</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1824131115542"><a name="p1824131115542"></a><a name="p1824131115542"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p28243118546"><a name="p28243118546"></a><a name="p28243118546"></a>-</p>
</td>
</tr>
<tr id="row20824311115419"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p12824121185412"><a name="p12824121185412"></a><a name="p12824121185412"></a>fetchone – fetch next row of the query result</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p1382419110543"><a name="p1382419110543"></a><a name="p1382419110543"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p8824911145412"><a name="p8824911145412"></a><a name="p8824911145412"></a>-</p>
</td>
</tr>
<tr id="row68251511125415"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p18825181155420"><a name="p18825181155420"></a><a name="p18825181155420"></a>fetchmany – fetch next set of rows of the query result</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p16825191111545"><a name="p16825191111545"></a><a name="p16825191111545"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p48258118548"><a name="p48258118548"></a><a name="p48258118548"></a>-</p>
</td>
</tr>
<tr id="row8825211145411"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p282571113545"><a name="p282571113545"></a><a name="p282571113545"></a>fetchall – fetch all rows of the query result</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p082511115410"><a name="p082511115410"></a><a name="p082511115410"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1482521119544"><a name="p1482521119544"></a><a name="p1482521119544"></a>-</p>
</td>
</tr>
<tr id="row1382511110543"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p178250115544"><a name="p178250115544"></a><a name="p178250115544"></a>arraysize - the number of rows to fetch at a time</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p982541115412"><a name="p982541115412"></a><a name="p982541115412"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p108251911195412"><a name="p108251911195412"></a><a name="p108251911195412"></a>-</p>
</td>
</tr>
<tr id="row4825211195411"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p082521165418"><a name="p082521165418"></a><a name="p082521165418"></a>Methods and attributes that are not part of the standard</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p282510111544"><a name="p282510111544"></a><a name="p282510111544"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p282515115540"><a name="p282515115540"></a><a name="p282515115540"></a>-</p>
</td>
</tr>
<tr id="row15825201111543"><td class="cellrowborder" rowspan="2" valign="top" width="15%" headers="mcps1.2.5.1.1 "><p id="p12825121195416"><a name="p12825121195416"></a><a name="p12825121195416"></a>Type – Type objects and constructors</p>
</td>
<td class="cellrowborder" valign="top" width="65%" headers="mcps1.2.5.1.1 "><p id="p15825121175416"><a name="p15825121175416"></a><a name="p15825121175416"></a>Type constructors</p>
</td>
<td class="cellrowborder" valign="top" width="10%" headers="mcps1.2.5.1.2 "><p id="p168251811105411"><a name="p168251811105411"></a><a name="p168251811105411"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" width="10%" headers="mcps1.2.5.1.3 "><p id="p20825191118546"><a name="p20825191118546"></a><a name="p20825191118546"></a>-</p>
</td>
</tr>
<tr id="row0825161119542"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p682541145410"><a name="p682541145410"></a><a name="p682541145410"></a>Type objects</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p5825101185411"><a name="p5825101185411"></a><a name="p5825101185411"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p13825411105414"><a name="p13825411105414"></a><a name="p13825411105414"></a>-</p>
</td>
</tr>
</tbody>
</table>

## 在Linux环境使用PyGreSQL第三方库连接集群<a name="section1331571718565"></a>

1.  以**root**用户登录Linux环境。
2.  执行以下命令创建python\_dws.py文件。

    ```
    vi python_dws.py
    ```

    请复制粘贴以下内容放入python\_dws.py文件中：

    ```
    #!/usr/bin/env python3
    # _*_ encoding:utf-8 _*_
     
    from __future__ import print_function
     
    import pg
     
     
    def create_table(connection):
        print("Begin to create table")
        try:
            connection.query("drop table if exists test;"
                             "create table test(id int, name text);")
        except pg.InternalError as e:
            print(e)
        else:
            print("Table created successfully")
     
     
    def insert_data(connection):
        print("Begin to insert data")
        try:
            connection.query("insert into test values(1,'number1');")
            connection.query("insert into test values(2,'number2');")
            connection.query("insert into test values(3,'number3');")
        except pg.InternalError as e:
            print(e)
        else:
            print("Insert data successfully")
     
     
    def update_data(connection):
        print("Begin to update data")
        try:
            result = connection.query("update test set name = 'numberupdated' where id=1;")
            print("Total number of rows updated :", result)
            result = connection.query("select * from test order by 1;")
            rows = result.getresult()
            for row in rows:
                print("id = ", row[0])
                print("name = ", row[1], "\n")
        except pg.InternalError as e:
            print(e)
        else:
            print("After Update, Operation done successfully")
     
     
    def delete_data(connection):
        print("Begin to delete data")
        try:
            result = connection.query("delete from test where id=3;")
            print("Total number of rows deleted :", result)
            result = connection.query("select * from test order by 1;")
            rows = result.getresult()
            for row in rows:
                print("id = ", row[0])
                print("name = ", row[1], "\n")
        except pg.InternalError as e:
            print(e)
        else:
            print("After Delete,Operation done successfully")
     
     
    def select_data(connection):
        print("Begin to select data")
        try:
            result = connection.query("select * from test order by 1;")
            rows = result.getresult()
            for row in rows:
                print("id = ", row[0])
                print("name = ", row[1])
        except pg.InternalError as e:
            print(e)
            print("select failed")
        else:
            print("Operation done successfully")
     
     
    if __name__ == '__main__':
        try:
            conn = pg.DB(host='10.154.70.231',
                         port=8000,
                         dbname='gaussdb', # 需要连接的database
                         user='dbadmin',
                         passwd='password')  # 数据库用户密码
        except pg.InternalError as ex:
            print(ex)
            print("Connect database failed")
        else:
            print("Opened database successfully")
            create_table(conn)
            insert_data(conn)
            select_data(conn)
            update_data(conn)
            delete_data(conn)
            conn.close()
    ```

    或使用dbapi接口实现：

    ```
    #!/usr/bin/python
    # -*- coding: UTF-8 -*-
     
    from __future__ import print_function
     
    import pg
    import pgdb
     
     
    def create_table(connection):
        print("Begin to create table")
        try:
            cursor = connection.cursor()
            cursor.execute("drop table if exists test;"
                           "create table test(id int, name text);")
            connection.commit()
        except pg.InternalError as e:
            print(e)
        else:
            print("Table created successfully")
            cursor.close()
     
     
    def insert_data(connection):
        print("Begin to insert data")
        try:
            cursor = connection.cursor()
            cursor.execute("insert into test values(1,'number1');")
            cursor.execute("insert into test values(2,'number2');")
            cursor.execute("insert into test values(3,'number3');")
            connection.commit()
        except pg.InternalError as e:
            print(e)
        else:
            print("Insert data successfully")
            cursor.close()
     
     
    def update_data(connection):
        print("Begin to update data")
        try:
            cursor = connection.cursor()
            cursor.execute("update test set name = 'numberupdated' where id=1;")
            connection.commit()
            print("Total number of rows updated :", cursor.rowcount)
            cursor.execute("select * from test;")
            rows = cursor.fetchall()
            for row in rows:
                print("id = ", row[0])
                print("name = ", row[1], "\n")
        except pg.InternalError as e:
            print(e)
        else:
            print("After Update, Operation done successfully")
     
     
    def delete_data(connection):
        print("Begin to delete data")
        try:
            cursor = connection.cursor()
            cursor.execute("delete from test where id=3;")
            connection.commit()
            print("Total number of rows deleted :", cursor.rowcount)
            cursor.execute("select * from test;")
            rows = cursor.fetchall()
            for row in rows:
                print("id = ", row[0])
                print("name = ", row[1], "\n")
        except pg.InternalError as e:
            print(e)
        else:
            print("After Delete,Operation done successfully")
     
     
    def select_data(connection):
        print("Begin to select data")
        try:
            cursor = connection.cursor()
            cursor.execute("select * from test;")
            rows = cursor.fetchall()
            for row in rows:
                print("id = ", row[0])
                print("name = ", row[1], "\n")
        except pg.InternalError as e:
            print(e)
            print("select failed")
        else:
            print("Operation done successfully")
            cursor.close()
     
     
    if __name__ == '__main__':
        try:
            conn = pgdb.connect(host='10.154.70.231',
                                          port='8000',
                                          database='gaussdb', # 需要连接的database
                                          user='dbadmin',
                                          password='password') # 数据库用户密码
        except pg.InternalError as ex:
            print(ex)
            print("Connect database failed")
        else:
            print("Opened database successfully")
            create_table(conn)
            insert_data(conn)
            select_data(conn)
            update_data(conn)
            delete_data(conn)
            conn.close()
    ```

3.  按照实际集群信息，修改python\_dws.py文件中的集群公网访问地址、集群端口号、数据库名称、数据库用户名、数据库密码。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >PyGreSQL接口不提供重试连接的能力，您需要在业务代码中实现重试处理。

    ```
            conn = pgdb.connect(host='10.154.70.231',
                                          port='8000',
                                          database='gaussdb', # 需要连接的database
                                          user='dbadmin',
                                          password='password') # 数据库用户密码
    ```

4.  执行以下命令，使用PyGreSQL第三方库连接集群。

    ```
    python python_dws.py
    ```


## 在Windows环境使用PyGreSQL第三方库连接集群<a name="section17342517105618"></a>

1.  在Windows系统中，单击“开始”按钮 ，在搜索框中，键入**cmd**，然后在结果列表中单击“cmd.exe”打开命令提示符窗口。
2.  在命令提示符窗口中，执行以下命令创建python\_dws.py文件。

    ```
    type nul> python_dws.py
    ```

    请复制粘贴以下内容放入python\_dws.py文件中：

    ```
    #!/usr/bin/env python3
    # _*_ encoding:utf-8 _*_
     
    from __future__ import print_function
     
    import pg
     
     
    def create_table(connection):
        print("Begin to create table")
        try:
            connection.query("drop table if exists test;"
                             "create table test(id int, name text);")
        except pg.InternalError as e:
            print(e)
        else:
            print("Table created successfully")
     
     
    def insert_data(connection):
        print("Begin to insert data")
        try:
            connection.query("insert into test values(1,'number1');")
            connection.query("insert into test values(2,'number2');")
            connection.query("insert into test values(3,'number3');")
        except pg.InternalError as e:
            print(e)
        else:
            print("Insert data successfully")
     
     
    def update_data(connection):
        print("Begin to update data")
        try:
            result = connection.query("update test set name = 'numberupdated' where id=1;")
            print("Total number of rows updated :", result)
            result = connection.query("select * from test order by 1;")
            rows = result.getresult()
            for row in rows:
                print("id = ", row[0])
                print("name = ", row[1], "\n")
        except pg.InternalError as e:
            print(e)
        else:
            print("After Update, Operation done successfully")
     
     
    def delete_data(connection):
        print("Begin to delete data")
        try:
            result = connection.query("delete from test where id=3;")
            print("Total number of rows deleted :", result)
            result = connection.query("select * from test order by 1;")
            rows = result.getresult()
            for row in rows:
                print("id = ", row[0])
                print("name = ", row[1], "\n")
        except pg.InternalError as e:
            print(e)
        else:
            print("After Delete,Operation done successfully")
     
     
    def select_data(connection):
        print("Begin to select data")
        try:
            result = connection.query("select * from test order by 1;")
            rows = result.getresult()
            for row in rows:
                print("id = ", row[0])
                print("name = ", row[1])
        except pg.InternalError as e:
            print(e)
            print("select failed")
        else:
            print("Operation done successfully")
     
     
    if __name__ == '__main__':
        try:
            conn = pg.DB(host='10.154.70.231',
                         port=8000,
                         dbname='gaussdb', # 需要连接的database
                         user='dbadmin',
                         passwd='password')  # 数据库用户密码
        except pg.InternalError as ex:
            print(ex)
            print("Connect database failed")
        else:
            print("Opened database successfully")
            create_table(conn)
            insert_data(conn)
            select_data(conn)
            update_data(conn)
            delete_data(conn)
            conn.close()
    ```

    或使用dbapi接口实现：：

    ```
    #!/usr/bin/python
    # -*- coding: UTF-8 -*-
     
    from __future__ import print_function
     
    import pg
    import pgdb
     
     
    def create_table(connection):
        print("Begin to create table")
        try:
            cursor = connection.cursor()
            cursor.execute("drop table if exists test;"
                           "create table test(id int, name text);")
            connection.commit()
        except pg.InternalError as e:
            print(e)
        else:
            print("Table created successfully")
            cursor.close()
     
     
    def insert_data(connection):
        print("Begin to insert data")
        try:
            cursor = connection.cursor()
            cursor.execute("insert into test values(1,'number1');")
            cursor.execute("insert into test values(2,'number2');")
            cursor.execute("insert into test values(3,'number3');")
            connection.commit()
        except pg.InternalError as e:
            print(e)
        else:
            print("Insert data successfully")
            cursor.close()
     
     
    def update_data(connection):
        print("Begin to update data")
        try:
            cursor = connection.cursor()
            cursor.execute("update test set name = 'numberupdated' where id=1;")
            connection.commit()
            print("Total number of rows updated :", cursor.rowcount)
            cursor.execute("select * from test;")
            rows = cursor.fetchall()
            for row in rows:
                print("id = ", row[0])
                print("name = ", row[1], "\n")
        except pg.InternalError as e:
            print(e)
        else:
            print("After Update, Operation done successfully")
     
     
    def delete_data(connection):
        print("Begin to delete data")
        try:
            cursor = connection.cursor()
            cursor.execute("delete from test where id=3;")
            connection.commit()
            print("Total number of rows deleted :", cursor.rowcount)
            cursor.execute("select * from test;")
            rows = cursor.fetchall()
            for row in rows:
                print("id = ", row[0])
                print("name = ", row[1], "\n")
        except pg.InternalError as e:
            print(e)
        else:
            print("After Delete,Operation done successfully")
     
     
    def select_data(connection):
        print("Begin to select data")
        try:
            cursor = connection.cursor()
            cursor.execute("select * from test;")
            rows = cursor.fetchall()
            for row in rows:
                print("id = ", row[0])
                print("name = ", row[1], "\n")
        except pg.InternalError as e:
            print(e)
            print("select failed")
        else:
            print("Operation done successfully")
            cursor.close()
     
     
    if __name__ == '__main__':
        try:
            conn = pgdb.connect(host='10.154.70.231',
                                          port='8000',
                                          database='gaussdb', # 需要连接的database
                                          user='dbadmin',
                                          password='password') # 数据库用户密码
        except pg.InternalError as ex:
            print(ex)
            print("Connect database failed")
        else:
            print("Opened database successfully")
            create_table(conn)
            insert_data(conn)
            select_data(conn)
            update_data(conn)
            delete_data(conn)
            conn.close()
    ```

3.  按照实际集群信息，修改python\_dws.py文件中的集群公网访问地址、集群端口号、数据库名称、数据库用户名、数据库密码。

    PyGreSQL接口不提供重试连接的能力，您需要在业务代码中实现重试处理。

    ```
            conn = pgdb.connect(host='10.154.70.231',
                                          port='8000',
                                          database='gaussdb', # 需要连接的database
                                          user='dbadmin',
                                          password='password') # 数据库用户密码
    ```

4.  执行以下命令，使用PyGreSQL第三方库连接集群。

    ```
    python python_dws.py
    ```


