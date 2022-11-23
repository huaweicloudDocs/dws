# 使用Python第三方库psycopg2连接集群<a name="ZH-CN_TOPIC_0000001405317086"></a>

用户在创建好数据仓库集群后使用psycopg2第三方库连接到集群，则可以使用Python访问GaussDB\(DWS\) ，并进行数据表的各类操作。

## 连接集群前的准备<a name="section5781841515252"></a>

-   GaussDB\(DWS\) 集群已绑定弹性IP。
-   已获取GaussDB\(DWS\) 集群的数据库管理员用户名和密码。

    请注意，由于MD5算法已经被证实存在碰撞可能，已严禁将之用于密码校验算法。当前GaussDB\(DWS\) 采用默认安全设计，默认禁止MD5算法的密码校验，可能导致开源客户端无法正常连接的问题。建议先检查一下数据库参数password\_encryption\_type参数是否为1，如果取值不为1，需要修改，修改方法参见[修改数据库参数](https://support.huaweicloud.com/mgtg-dws/dws_01_0152.html)；然后修改一次准备使用的数据库用户的密码。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   当前GaussDB\(DWS\)出于安全考虑，已经默认不再使用MD5存储密码摘要了，这将导致使用开源驱动或者客户端无法正常连接数据库。需要您调整一下密码策略后再创建一个新用户或者对老用户做一次密码修改，方可使用开源协议中的MD5认证算法。
    >-   数据库中是不会存储用户的密码原文，而是存储密码的HASH摘要，在密码校验时与客户端发来的密码摘要进行比对（中间会有加盐操作）。故当您改变了密码算法策略时，数据库也是无法还原您的密码，再生成新的HASH算法的摘要值的。必须您手动修改一次密码或者创建一个新用户，这时新的密码将会采用您设置的HASH算法进行摘要存储，用于下次连接认证。

-   已获取GaussDB\(DWS\) 集群的公网访问地址，含IP地址和端口。具体请参见[获取集群连接地址](获取集群连接地址.md)。
-   已安装psycopg2第三方库。下载地址：[https://pypi.org/project/psycopg2/](https://pypi.org/project/psycopg2/)，安装部署操作请参见：[https://www.psycopg.org/install/](https://www.psycopg.org/install/)。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   CentOS、Redhat等操作系统中使用yum命令安装，命令为：
    >    ```
    >    yum install python-psycopg2
    >    ```
    >-   psycopg2的使用依赖于PostgreSQL的libpq动态库（32位的psycopg2需要对应32位的libpq；64位的psycopg2对应64位的libpq），Linux中可以依赖yum命令解决。在Windows系统使用psycopg2需要先安装libpq，主要方式有两种：
    >    -   安装PostgreSQL，并配置libpq、ssl、crypto动态库位置到环境变量PATH中。
    >    -   安装psqlodbc，使用PostgreSQL ODBC驱动携带的libpq、ssl、crypto动态库。


## 使用约束<a name="section346571443710"></a>

由于psycopg2是基于PostgreSQL的客户端接口，它的功能GaussDB\(DWS\)并不能完全支持。具体支持情况请见下[表1](#table147698595445)。

>![](public_sys-resources/icon-note.gif) **说明：** 
>以下接口支持情况是基于Python 3.8.5及psycopg 2.9.1版本。

**表 1**  DWS对psycopg2主要接口支持情况

<a name="table147698595445"></a>
<table><thead align="left"><tr id="row15912159104419"><th class="cellrowborder" valign="top" width="15.459999999999999%" id="mcps1.2.6.1.1"><p id="p1912135964417"><a name="p1912135964417"></a><a name="p1912135964417"></a>类名</p>
</th>
<th class="cellrowborder" valign="top" width="15.459999999999999%" id="mcps1.2.6.1.2"><p id="p199129591441"><a name="p199129591441"></a><a name="p199129591441"></a>功能描述</p>
</th>
<th class="cellrowborder" valign="top" width="39.18%" id="mcps1.2.6.1.3"><p id="p29128596444"><a name="p29128596444"></a><a name="p29128596444"></a>函数/成员变量</p>
</th>
<th class="cellrowborder" valign="top" width="9.28%" id="mcps1.2.6.1.4"><p id="p1091218598446"><a name="p1091218598446"></a><a name="p1091218598446"></a>支持</p>
</th>
<th class="cellrowborder" valign="top" width="20.62%" id="mcps1.2.6.1.5"><p id="p79123597448"><a name="p79123597448"></a><a name="p79123597448"></a>备注</p>
</th>
</tr>
</thead>
<tbody><tr id="row199127594448"><td class="cellrowborder" rowspan="39" valign="top" width="15.459999999999999%" headers="mcps1.2.6.1.1 "><p id="p1891245934416"><a name="p1891245934416"></a><a name="p1891245934416"></a>connections</p>
</td>
<td class="cellrowborder" rowspan="4" valign="top" width="15.459999999999999%" headers="mcps1.2.6.1.2 "><p id="p13912195994410"><a name="p13912195994410"></a><a name="p13912195994410"></a>basic</p>
</td>
<td class="cellrowborder" valign="top" width="39.18%" headers="mcps1.2.6.1.3 "><p id="p291212596443"><a name="p291212596443"></a><a name="p291212596443"></a>cursor(<em id="i891295911447"><a name="i891295911447"></a><a name="i891295911447"></a>name=None</em>, <em id="i139123591448"><a name="i139123591448"></a><a name="i139123591448"></a>cursor_factory=None</em>, <em id="i119121759184413"><a name="i119121759184413"></a><a name="i119121759184413"></a>scrollable=None</em>, <em id="i139121159184418"><a name="i139121159184418"></a><a name="i139121159184418"></a>withhold=False</em>)</p>
</td>
<td class="cellrowborder" valign="top" width="9.28%" headers="mcps1.2.6.1.4 "><p id="p391265904418"><a name="p391265904418"></a><a name="p391265904418"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" width="20.62%" headers="mcps1.2.6.1.5 "><p id="p12912165912443"><a name="p12912165912443"></a><a name="p12912165912443"></a>-</p>
</td>
</tr>
<tr id="row2912175974413"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p1291210599441"><a name="p1291210599441"></a><a name="p1291210599441"></a>commit()</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p1391235914420"><a name="p1391235914420"></a><a name="p1391235914420"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p14913175904416"><a name="p14913175904416"></a><a name="p14913175904416"></a>-</p>
</td>
</tr>
<tr id="row4913205924416"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p391316597447"><a name="p391316597447"></a><a name="p391316597447"></a>rollback()</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p11913659104416"><a name="p11913659104416"></a><a name="p11913659104416"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p1791316593441"><a name="p1791316593441"></a><a name="p1791316593441"></a>-</p>
</td>
</tr>
<tr id="row11913155944416"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p1091316596445"><a name="p1091316596445"></a><a name="p1091316596445"></a>close()</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p6913559124418"><a name="p6913559124418"></a><a name="p6913559124418"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p5913165984417"><a name="p5913165984417"></a><a name="p5913165984417"></a>-</p>
</td>
</tr>
<tr id="row3913175964416"><td class="cellrowborder" rowspan="10" valign="top" headers="mcps1.2.6.1.1 "><p id="p291365910446"><a name="p291365910446"></a><a name="p291365910446"></a>Two-phase commit support methods</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p18913459114411"><a name="p18913459114411"></a><a name="p18913459114411"></a>xid(<em id="i17913559184413"><a name="i17913559184413"></a><a name="i17913559184413"></a>format_id</em>, <em id="i9913155918443"><a name="i9913155918443"></a><a name="i9913155918443"></a>gtrid</em>, <em id="i1913259104420"><a name="i1913259104420"></a><a name="i1913259104420"></a>bqual</em>)</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p7913175915443"><a name="p7913175915443"></a><a name="p7913175915443"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.4 "><p id="p149134596440"><a name="p149134596440"></a><a name="p149134596440"></a>-</p>
</td>
</tr>
<tr id="row149131259184419"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p3913205954410"><a name="p3913205954410"></a><a name="p3913205954410"></a>tpc_begin(<em id="i1591319594442"><a name="i1591319594442"></a><a name="i1591319594442"></a>xid</em>)</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p159131259114419"><a name="p159131259114419"></a><a name="p159131259114419"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p791313591441"><a name="p791313591441"></a><a name="p791313591441"></a>-</p>
</td>
</tr>
<tr id="row1791395916441"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p891317592449"><a name="p891317592449"></a><a name="p891317592449"></a>tpc_prepare()</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p10913859134412"><a name="p10913859134412"></a><a name="p10913859134412"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p6913145918447"><a name="p6913145918447"></a><a name="p6913145918447"></a>内核不支持显式prepare transaction</p>
</td>
</tr>
<tr id="row209130592443"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p10913159134413"><a name="p10913159134413"></a><a name="p10913159134413"></a>tpc_commit([<em id="i20913759114419"><a name="i20913759114419"></a><a name="i20913759114419"></a>xid</em>])</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p1491305954410"><a name="p1491305954410"></a><a name="p1491305954410"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p391314597443"><a name="p391314597443"></a><a name="p391314597443"></a>-</p>
</td>
</tr>
<tr id="row1913185964415"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p8913105944419"><a name="p8913105944419"></a><a name="p8913105944419"></a>tpc_rollback([<em id="i1491385911440"><a name="i1491385911440"></a><a name="i1491385911440"></a>xid</em>])</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p1091415919441"><a name="p1091415919441"></a><a name="p1091415919441"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p39141559134418"><a name="p39141559134418"></a><a name="p39141559134418"></a>-</p>
</td>
</tr>
<tr id="row49141759164416"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p18914115913449"><a name="p18914115913449"></a><a name="p18914115913449"></a>tpc_recover()</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p291425924414"><a name="p291425924414"></a><a name="p291425924414"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p29141359104411"><a name="p29141359104411"></a><a name="p29141359104411"></a>-</p>
</td>
</tr>
<tr id="row1791475914447"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p7914059144419"><a name="p7914059144419"></a><a name="p7914059144419"></a>closed</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p79147598444"><a name="p79147598444"></a><a name="p79147598444"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p7914185974412"><a name="p7914185974412"></a><a name="p7914185974412"></a>-</p>
</td>
</tr>
<tr id="row3914195994412"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p991414593444"><a name="p991414593444"></a><a name="p991414593444"></a>cancel()</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p6914105994418"><a name="p6914105994418"></a><a name="p6914105994418"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p139141559124412"><a name="p139141559124412"></a><a name="p139141559124412"></a>-</p>
</td>
</tr>
<tr id="row149141359114418"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p5914205964419"><a name="p5914205964419"></a><a name="p5914205964419"></a>reset()</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p0914459154418"><a name="p0914459154418"></a><a name="p0914459154418"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p591445914420"><a name="p591445914420"></a><a name="p591445914420"></a>不支持DISCARD ALL</p>
</td>
</tr>
<tr id="row14914195911444"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p17914185994420"><a name="p17914185994420"></a><a name="p17914185994420"></a>dsn</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p11914185916441"><a name="p11914185916441"></a><a name="p11914185916441"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p391495916441"><a name="p391495916441"></a><a name="p391495916441"></a>-</p>
</td>
</tr>
<tr id="row1914165913448"><td class="cellrowborder" rowspan="14" valign="top" headers="mcps1.2.6.1.1 "><p id="p3914175912444"><a name="p3914175912444"></a><a name="p3914175912444"></a>Transaction control methods and attributes.</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p1891455913445"><a name="p1891455913445"></a><a name="p1891455913445"></a>set_session(<em id="i1491419596447"><a name="i1491419596447"></a><a name="i1491419596447"></a>isolation_level=None</em>, <em id="i491485944415"><a name="i491485944415"></a><a name="i491485944415"></a>readonly=None</em>, <em id="i89141359184416"><a name="i89141359184416"></a><a name="i89141359184416"></a>deferrable=None</em>, <em id="i39141559184410"><a name="i39141559184410"></a><a name="i39141559184410"></a>autocommit=None</em>)</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p169141759194410"><a name="p169141759194410"></a><a name="p169141759194410"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.4 "><p id="p14914559194412"><a name="p14914559194412"></a><a name="p14914559194412"></a>数据库不支持session中设置default_transaction_read_only</p>
</td>
</tr>
<tr id="row3914135915443"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p1191425924416"><a name="p1191425924416"></a><a name="p1191425924416"></a>autocommit</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p16914059204414"><a name="p16914059204414"></a><a name="p16914059204414"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p791475920445"><a name="p791475920445"></a><a name="p791475920445"></a>-</p>
</td>
</tr>
<tr id="row591513595443"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p89151759154411"><a name="p89151759154411"></a><a name="p89151759154411"></a>isolation_level</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p391514592449"><a name="p391514592449"></a><a name="p391514592449"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p11915185910442"><a name="p11915185910442"></a><a name="p11915185910442"></a>-</p>
</td>
</tr>
<tr id="row29159599446"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p991535974420"><a name="p991535974420"></a><a name="p991535974420"></a>readonly</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p791525934412"><a name="p791525934412"></a><a name="p791525934412"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p1891535917447"><a name="p1891535917447"></a><a name="p1891535917447"></a>数据库不支持session中设置default_transaction_read_only</p>
</td>
</tr>
<tr id="row391595934416"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p1291516595446"><a name="p1291516595446"></a><a name="p1291516595446"></a>deferrable</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p109151659174420"><a name="p109151659174420"></a><a name="p109151659174420"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p17915659114411"><a name="p17915659114411"></a><a name="p17915659114411"></a>-</p>
</td>
</tr>
<tr id="row7915559154414"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p2915859164415"><a name="p2915859164415"></a><a name="p2915859164415"></a>set_isolation_level(<em id="i12915185914445"><a name="i12915185914445"></a><a name="i12915185914445"></a>level</em>)</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p991575916440"><a name="p991575916440"></a><a name="p991575916440"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p39151359154412"><a name="p39151359154412"></a><a name="p39151359154412"></a>-</p>
</td>
</tr>
<tr id="row14915259114418"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p49156592446"><a name="p49156592446"></a><a name="p49156592446"></a>encoding</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p29154599441"><a name="p29154599441"></a><a name="p29154599441"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p791585904417"><a name="p791585904417"></a><a name="p791585904417"></a>-</p>
</td>
</tr>
<tr id="row991517597442"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p4915059134415"><a name="p4915059134415"></a><a name="p4915059134415"></a>set_client_encoding(enc)</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p5915135919440"><a name="p5915135919440"></a><a name="p5915135919440"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p19151259114418"><a name="p19151259114418"></a><a name="p19151259114418"></a>-</p>
</td>
</tr>
<tr id="row791545916449"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p2915205994410"><a name="p2915205994410"></a><a name="p2915205994410"></a>notices</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p1891595919441"><a name="p1891595919441"></a><a name="p1891595919441"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p1491575974411"><a name="p1491575974411"></a><a name="p1491575974411"></a>数据库不支持listen/notify</p>
</td>
</tr>
<tr id="row169150594446"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p1891575914447"><a name="p1891575914447"></a><a name="p1891575914447"></a>notifies</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p169151359194414"><a name="p169151359194414"></a><a name="p169151359194414"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p19915185994419"><a name="p19915185994419"></a><a name="p19915185994419"></a>-</p>
</td>
</tr>
<tr id="row1291555911449"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p10916125934416"><a name="p10916125934416"></a><a name="p10916125934416"></a>cursor_factory</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p691611595442"><a name="p691611595442"></a><a name="p691611595442"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p6916125910441"><a name="p6916125910441"></a><a name="p6916125910441"></a>-</p>
</td>
</tr>
<tr id="row17916159114416"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p99161459194414"><a name="p99161459194414"></a><a name="p99161459194414"></a>info</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p1691619599442"><a name="p1691619599442"></a><a name="p1691619599442"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p109164594441"><a name="p109164594441"></a><a name="p109164594441"></a>-</p>
</td>
</tr>
<tr id="row109161359154420"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p1791655994416"><a name="p1791655994416"></a><a name="p1791655994416"></a>status</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p99164597444"><a name="p99164597444"></a><a name="p99164597444"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p8916259174420"><a name="p8916259174420"></a><a name="p8916259174420"></a>-</p>
</td>
</tr>
<tr id="row16916359134410"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p291645904419"><a name="p291645904419"></a><a name="p291645904419"></a>lobject</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p4916105994418"><a name="p4916105994418"></a><a name="p4916105994418"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p16916165912449"><a name="p16916165912449"></a><a name="p16916165912449"></a>数据库不支持大对象相关操作</p>
</td>
</tr>
<tr id="row491685916445"><td class="cellrowborder" rowspan="3" valign="top" headers="mcps1.2.6.1.1 "><p id="p791615599448"><a name="p791615599448"></a><a name="p791615599448"></a>Methods related to asynchronous support</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p13916759144410"><a name="p13916759144410"></a><a name="p13916759144410"></a>poll()</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p159166594447"><a name="p159166594447"></a><a name="p159166594447"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.4 "><p id="p2916159164415"><a name="p2916159164415"></a><a name="p2916159164415"></a>-</p>
</td>
</tr>
<tr id="row69161959154416"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p159161559194419"><a name="p159161559194419"></a><a name="p159161559194419"></a>fileno()</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p191695919444"><a name="p191695919444"></a><a name="p191695919444"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p5916459114415"><a name="p5916459114415"></a><a name="p5916459114415"></a>-</p>
</td>
</tr>
<tr id="row159164595449"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p991685964416"><a name="p991685964416"></a><a name="p991685964416"></a>isexecuting()</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p20916195911449"><a name="p20916195911449"></a><a name="p20916195911449"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p18916165914419"><a name="p18916165914419"></a><a name="p18916165914419"></a>-</p>
</td>
</tr>
<tr id="row09161759134417"><td class="cellrowborder" rowspan="2" valign="top" headers="mcps1.2.6.1.1 "><p id="p15916195954415"><a name="p15916195954415"></a><a name="p15916195954415"></a>Interoperation with other C API modules</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p491605974410"><a name="p491605974410"></a><a name="p491605974410"></a>pgconn_ptr</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p1916165917443"><a name="p1916165917443"></a><a name="p1916165917443"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.4 "><p id="p09169593447"><a name="p09169593447"></a><a name="p09169593447"></a>-</p>
</td>
</tr>
<tr id="row129161659134417"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p691716593445"><a name="p691716593445"></a><a name="p691716593445"></a>get_native_connection()</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p091718597444"><a name="p091718597444"></a><a name="p091718597444"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p1891705918446"><a name="p1891705918446"></a><a name="p1891705918446"></a>-</p>
</td>
</tr>
<tr id="row991715591446"><td class="cellrowborder" rowspan="6" valign="top" headers="mcps1.2.6.1.1 "><p id="p79172059114411"><a name="p79172059114411"></a><a name="p79172059114411"></a>informative methods of the native connection</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p4917959134413"><a name="p4917959134413"></a><a name="p4917959134413"></a>get_transaction_status()</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p99171759144410"><a name="p99171759144410"></a><a name="p99171759144410"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.4 "><p id="p7917125914446"><a name="p7917125914446"></a><a name="p7917125914446"></a>-</p>
</td>
</tr>
<tr id="row15917105910447"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p12917959164420"><a name="p12917959164420"></a><a name="p12917959164420"></a>protocol_version</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p119171759124418"><a name="p119171759124418"></a><a name="p119171759124418"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p49171759204419"><a name="p49171759204419"></a><a name="p49171759204419"></a>-</p>
</td>
</tr>
<tr id="row7917115913446"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p6917459194419"><a name="p6917459194419"></a><a name="p6917459194419"></a>server_version</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p1291775911440"><a name="p1291775911440"></a><a name="p1291775911440"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p891715914418"><a name="p891715914418"></a><a name="p891715914418"></a>-</p>
</td>
</tr>
<tr id="row6917165912449"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p391711597441"><a name="p391711597441"></a><a name="p391711597441"></a>get_backend_pid()</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p16917115913441"><a name="p16917115913441"></a><a name="p16917115913441"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p1291775919446"><a name="p1291775919446"></a><a name="p1291775919446"></a>获取到的不是后台的pid，是逻辑连接的id号</p>
</td>
</tr>
<tr id="row19917155913442"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p189171959144419"><a name="p189171959144419"></a><a name="p189171959144419"></a>get_parameter_status(parameter)</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p1691715917448"><a name="p1691715917448"></a><a name="p1691715917448"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p591705944411"><a name="p591705944411"></a><a name="p591705944411"></a>-</p>
</td>
</tr>
<tr id="row191715594445"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p59176591442"><a name="p59176591442"></a><a name="p59176591442"></a>get_dsn_parameters()</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p1917125914418"><a name="p1917125914418"></a><a name="p1917125914418"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p19179598442"><a name="p19179598442"></a><a name="p19179598442"></a>-</p>
</td>
</tr>
<tr id="row391745984412"><td class="cellrowborder" rowspan="31" valign="top" width="15.459999999999999%" headers="mcps1.2.6.1.1 "><p id="p12917115984415"><a name="p12917115984415"></a><a name="p12917115984415"></a>cursor</p>
</td>
<td class="cellrowborder" rowspan="7" valign="top" width="15.459999999999999%" headers="mcps1.2.6.1.2 "><p id="p791795911443"><a name="p791795911443"></a><a name="p791795911443"></a>basic</p>
</td>
<td class="cellrowborder" valign="top" width="39.18%" headers="mcps1.2.6.1.3 "><p id="p1791765915445"><a name="p1791765915445"></a><a name="p1791765915445"></a>description</p>
</td>
<td class="cellrowborder" valign="top" width="9.28%" headers="mcps1.2.6.1.4 "><p id="p39179596445"><a name="p39179596445"></a><a name="p39179596445"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" width="20.62%" headers="mcps1.2.6.1.5 "><p id="p3918115994415"><a name="p3918115994415"></a><a name="p3918115994415"></a>-</p>
</td>
</tr>
<tr id="row1391825934412"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p691810593448"><a name="p691810593448"></a><a name="p691810593448"></a>close()</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p39181590445"><a name="p39181590445"></a><a name="p39181590445"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p191815912448"><a name="p191815912448"></a><a name="p191815912448"></a>-</p>
</td>
</tr>
<tr id="row4918559154418"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p16918959204413"><a name="p16918959204413"></a><a name="p16918959204413"></a>closed</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p14918859124414"><a name="p14918859124414"></a><a name="p14918859124414"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p11918175934417"><a name="p11918175934417"></a><a name="p11918175934417"></a>-</p>
</td>
</tr>
<tr id="row18918759194414"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p159181459184419"><a name="p159181459184419"></a><a name="p159181459184419"></a>connection</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p091825904415"><a name="p091825904415"></a><a name="p091825904415"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p891855954418"><a name="p891855954418"></a><a name="p891855954418"></a>-</p>
</td>
</tr>
<tr id="row991825974418"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p99181659134415"><a name="p99181659134415"></a><a name="p99181659134415"></a>name</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p691835916440"><a name="p691835916440"></a><a name="p691835916440"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p49181959184412"><a name="p49181959184412"></a><a name="p49181959184412"></a>-</p>
</td>
</tr>
<tr id="row109181594445"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p159181659154414"><a name="p159181659154414"></a><a name="p159181659154414"></a>scrollable</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p09183591446"><a name="p09183591446"></a><a name="p09183591446"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p891825934416"><a name="p891825934416"></a><a name="p891825934416"></a>数据库不支持SCROLL CURSOR</p>
</td>
</tr>
<tr id="row29181959194415"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p9918175912443"><a name="p9918175912443"></a><a name="p9918175912443"></a>withhold</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p1991885918447"><a name="p1991885918447"></a><a name="p1991885918447"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p1091865914445"><a name="p1091865914445"></a><a name="p1091865914445"></a>withhold cursor在commit前需要关闭</p>
</td>
</tr>
<tr id="row1491812596441"><td class="cellrowborder" rowspan="20" valign="top" headers="mcps1.2.6.1.1 "><p id="p091819593448"><a name="p091819593448"></a><a name="p091819593448"></a>Commands execution methods</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p199184594441"><a name="p199184594441"></a><a name="p199184594441"></a>execute(<em id="i291835984416"><a name="i291835984416"></a><a name="i291835984416"></a>query</em>, <em id="i491818591449"><a name="i491818591449"></a><a name="i491818591449"></a>vars=None</em>)</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p18918205910444"><a name="p18918205910444"></a><a name="p18918205910444"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.4 "><p id="p1791845924410"><a name="p1791845924410"></a><a name="p1791845924410"></a>-</p>
</td>
</tr>
<tr id="row159181559154420"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p17919135915443"><a name="p17919135915443"></a><a name="p17919135915443"></a>executemany(<em id="i13919175913441"><a name="i13919175913441"></a><a name="i13919175913441"></a>query</em>, <em id="i0919125974411"><a name="i0919125974411"></a><a name="i0919125974411"></a>vars_list</em>)</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p8919759164411"><a name="p8919759164411"></a><a name="p8919759164411"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p159190591446"><a name="p159190591446"></a><a name="p159190591446"></a>-</p>
</td>
</tr>
<tr id="row3919175917445"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p1091911594447"><a name="p1091911594447"></a><a name="p1091911594447"></a>callproc(<em id="i3919159204418"><a name="i3919159204418"></a><a name="i3919159204418"></a>procname</em>[, <em id="i39197599446"><a name="i39197599446"></a><a name="i39197599446"></a>parameters</em>])</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p9919115984410"><a name="p9919115984410"></a><a name="p9919115984410"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p991935920446"><a name="p991935920446"></a><a name="p991935920446"></a>-</p>
</td>
</tr>
<tr id="row139197594442"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p9919259134413"><a name="p9919259134413"></a><a name="p9919259134413"></a>mogrify(<em id="i89191559174412"><a name="i89191559174412"></a><a name="i89191559174412"></a>operation</em>[, <em id="i1391905915443"><a name="i1391905915443"></a><a name="i1391905915443"></a>parameters</em>])</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p17919959144418"><a name="p17919959144418"></a><a name="p17919959144418"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p139191559174411"><a name="p139191559174411"></a><a name="p139191559174411"></a>-</p>
</td>
</tr>
<tr id="row391965934412"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p8919459204412"><a name="p8919459204412"></a><a name="p8919459204412"></a>setinputsizes(<em id="i17919155974410"><a name="i17919155974410"></a><a name="i17919155974410"></a>sizes</em>)</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p79191959124411"><a name="p79191959124411"></a><a name="p79191959124411"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p2919165913443"><a name="p2919165913443"></a><a name="p2919165913443"></a>-</p>
</td>
</tr>
<tr id="row3919135934415"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p69191592447"><a name="p69191592447"></a><a name="p69191592447"></a>fetchone()</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p59191859204414"><a name="p59191859204414"></a><a name="p59191859204414"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p1391914591446"><a name="p1391914591446"></a><a name="p1391914591446"></a>-</p>
</td>
</tr>
<tr id="row199191159154418"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p109195593440"><a name="p109195593440"></a><a name="p109195593440"></a>fetchmany([<em id="i1919959154417"><a name="i1919959154417"></a><a name="i1919959154417"></a>size=cursor.arraysize</em>])</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p3919155912447"><a name="p3919155912447"></a><a name="p3919155912447"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p17919105994415"><a name="p17919105994415"></a><a name="p17919105994415"></a>-</p>
</td>
</tr>
<tr id="row189191359114413"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p391915593447"><a name="p391915593447"></a><a name="p391915593447"></a>fetchall()</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p149191159134416"><a name="p149191159134416"></a><a name="p149191159134416"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p591995913445"><a name="p591995913445"></a><a name="p591995913445"></a>-</p>
</td>
</tr>
<tr id="row1491925916444"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p1192085912447"><a name="p1192085912447"></a><a name="p1192085912447"></a>scroll(<em id="i1892065924411"><a name="i1892065924411"></a><a name="i1892065924411"></a>value</em>[, <em id="i992019596443"><a name="i992019596443"></a><a name="i992019596443"></a>mode='relative'</em>])</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p392085910443"><a name="p392085910443"></a><a name="p392085910443"></a>N</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p1092085910442"><a name="p1092085910442"></a><a name="p1092085910442"></a>数据库不支持SCROLL CURSOR</p>
</td>
</tr>
<tr id="row49201659204416"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p0920135934417"><a name="p0920135934417"></a><a name="p0920135934417"></a>arraysize</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p1920145913444"><a name="p1920145913444"></a><a name="p1920145913444"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p892095913447"><a name="p892095913447"></a><a name="p892095913447"></a>-</p>
</td>
</tr>
<tr id="row17920959114414"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p149201459174415"><a name="p149201459174415"></a><a name="p149201459174415"></a>itersize</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p5920959124410"><a name="p5920959124410"></a><a name="p5920959124410"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p1892019599447"><a name="p1892019599447"></a><a name="p1892019599447"></a>-</p>
</td>
</tr>
<tr id="row159201159154419"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p11920135910441"><a name="p11920135910441"></a><a name="p11920135910441"></a>rowcount</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p1692035910448"><a name="p1692035910448"></a><a name="p1692035910448"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p119201259164415"><a name="p119201259164415"></a><a name="p119201259164415"></a>-</p>
</td>
</tr>
<tr id="row1392005974414"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p11920175954416"><a name="p11920175954416"></a><a name="p11920175954416"></a>rownumber</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p11920259114416"><a name="p11920259114416"></a><a name="p11920259114416"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p292015593443"><a name="p292015593443"></a><a name="p292015593443"></a>-</p>
</td>
</tr>
<tr id="row13920135914449"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p8920135904415"><a name="p8920135904415"></a><a name="p8920135904415"></a>lastrowid</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p10920159104416"><a name="p10920159104416"></a><a name="p10920159104416"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p129203598446"><a name="p129203598446"></a><a name="p129203598446"></a>-</p>
</td>
</tr>
<tr id="row99204595448"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p16920195913446"><a name="p16920195913446"></a><a name="p16920195913446"></a>query</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p199201559144413"><a name="p199201559144413"></a><a name="p199201559144413"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p19920195915447"><a name="p19920195915447"></a><a name="p19920195915447"></a>-</p>
</td>
</tr>
<tr id="row492010597446"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p159204592442"><a name="p159204592442"></a><a name="p159204592442"></a>statusmessage</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p0920159194410"><a name="p0920159194410"></a><a name="p0920159194410"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p16920175917447"><a name="p16920175917447"></a><a name="p16920175917447"></a>-</p>
</td>
</tr>
<tr id="row11920759114417"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p0920155915445"><a name="p0920155915445"></a><a name="p0920155915445"></a>cast(<em id="i139218596448"><a name="i139218596448"></a><a name="i139218596448"></a>oid</em>, <em id="i1092145954416"><a name="i1092145954416"></a><a name="i1092145954416"></a>s</em>)</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p19211459114412"><a name="p19211459114412"></a><a name="p19211459114412"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p392118592445"><a name="p392118592445"></a><a name="p392118592445"></a>-</p>
</td>
</tr>
<tr id="row7921659194419"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p13921105954419"><a name="p13921105954419"></a><a name="p13921105954419"></a>tzinfo_factory</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p1492145984414"><a name="p1492145984414"></a><a name="p1492145984414"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p9921205920442"><a name="p9921205920442"></a><a name="p9921205920442"></a>-</p>
</td>
</tr>
<tr id="row39211959184415"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p1492135904417"><a name="p1492135904417"></a><a name="p1492135904417"></a>nextset()</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p13921135910444"><a name="p13921135910444"></a><a name="p13921135910444"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p792155904414"><a name="p792155904414"></a><a name="p792155904414"></a>-</p>
</td>
</tr>
<tr id="row15921959194413"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p9921125917443"><a name="p9921125917443"></a><a name="p9921125917443"></a>setoutputsize(<em id="i6921115920442"><a name="i6921115920442"></a><a name="i6921115920442"></a>size</em>[, <em id="i14921125984415"><a name="i14921125984415"></a><a name="i14921125984415"></a>column</em>])</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p1792113590441"><a name="p1792113590441"></a><a name="p1792113590441"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p89219595446"><a name="p89219595446"></a><a name="p89219595446"></a>-</p>
</td>
</tr>
<tr id="row1092175910444"><td class="cellrowborder" rowspan="3" valign="top" headers="mcps1.2.6.1.1 "><p id="p179216595447"><a name="p179216595447"></a><a name="p179216595447"></a>COPY-related methods</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p29212596441"><a name="p29212596441"></a><a name="p29212596441"></a>copy_from(<em id="i169218592443"><a name="i169218592443"></a><a name="i169218592443"></a>file</em>, <em id="i14921185917445"><a name="i14921185917445"></a><a name="i14921185917445"></a>table</em>, <em id="i10921359174411"><a name="i10921359174411"></a><a name="i10921359174411"></a>sep='\\t'</em>, <em id="i892117593442"><a name="i892117593442"></a><a name="i892117593442"></a>null='\\\\N'</em>, <em id="i19211859154419"><a name="i19211859154419"></a><a name="i19211859154419"></a>size=8192</em>, <em id="i20921259154413"><a name="i20921259154413"></a><a name="i20921259154413"></a>columns=None</em>)</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p11921175934412"><a name="p11921175934412"></a><a name="p11921175934412"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.4 "><p id="p792117598448"><a name="p792117598448"></a><a name="p792117598448"></a>-</p>
</td>
</tr>
<tr id="row9921115914448"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p592135934413"><a name="p592135934413"></a><a name="p592135934413"></a>copy_to(<em id="i2921155911446"><a name="i2921155911446"></a><a name="i2921155911446"></a>file</em>, <em id="i492115919441"><a name="i492115919441"></a><a name="i492115919441"></a>table</em>, <em id="i49211259184413"><a name="i49211259184413"></a><a name="i49211259184413"></a>sep='\\t'</em>, <em id="i169211859114413"><a name="i169211859114413"></a><a name="i169211859114413"></a>null='\\\\N'</em>, <em id="i8922145917445"><a name="i8922145917445"></a><a name="i8922145917445"></a>columns=None</em>)</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p99222599443"><a name="p99222599443"></a><a name="p99222599443"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p092265920442"><a name="p092265920442"></a><a name="p092265920442"></a>-</p>
</td>
</tr>
<tr id="row139221259154419"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p1092235918447"><a name="p1092235918447"></a><a name="p1092235918447"></a>copy_expert(<em id="i199222594444"><a name="i199222594444"></a><a name="i199222594444"></a>sql</em>, <em id="i199220591443"><a name="i199220591443"></a><a name="i199220591443"></a>file</em>, <em id="i1492255920444"><a name="i1492255920444"></a><a name="i1492255920444"></a>size=8192</em>)</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p16922205924415"><a name="p16922205924415"></a><a name="p16922205924415"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p14922195915449"><a name="p14922195915449"></a><a name="p14922195915449"></a>-</p>
</td>
</tr>
<tr id="row1992255914445"><td class="cellrowborder" valign="top" headers="mcps1.2.6.1.1 "><p id="p592312599447"><a name="p592312599447"></a><a name="p592312599447"></a>Interoperation with other C API modules</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.2 "><p id="p17923125924415"><a name="p17923125924415"></a><a name="p17923125924415"></a>pgresult_ptr</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.3 "><p id="p7923135944415"><a name="p7923135944415"></a><a name="p7923135944415"></a>Y</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.6.1.4 "><p id="p149235590444"><a name="p149235590444"></a><a name="p149235590444"></a>-</p>
</td>
</tr>
</tbody>
</table>

## 在Linux环境使用psycopg2第三方库连接集群<a name="section2825650154610"></a>

1.  以**root**用户登录Linux环境。
2.  执行以下命令创建python\_dws.py文件。

    ```
    vi python_dws.py
    ```

    请复制粘贴以下内容放入python\_dws.py文件中：

    ```
    #!/usr/bin/python
    # -*- coding: UTF-8 -*-
     
    from __future__ import print_function
     
    import psycopg2
     
     
    def create_table(connection):
        print("Begin to create table")
        try:
            cursor = connection.cursor()
            cursor.execute("drop table if exists test;"
                           "create table test(id int, name text);")
            connection.commit()
        except psycopg2.ProgrammingError as e:
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
        except psycopg2.ProgrammingError as e:
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
            cursor.execute("select * from test order by 1;")
            rows = cursor.fetchall()
            for row in rows:
                print("id = ", row[0])
                print("name = ", row[1], "\n")
        except psycopg2.ProgrammingError as e:
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
            cursor.execute("select * from test order by 1;")
            rows = cursor.fetchall()
            for row in rows:
                print("id = ", row[0])
                print("name = ", row[1], "\n")
        except psycopg2.ProgrammingError as e:
            print(e)
        else:
            print("After Delete,Operation done successfully")
     
     
    def select_data(connection):
        print("Begin to select data")
        try:
            cursor = connection.cursor()
            cursor.execute("select * from test order by 1;")
            rows = cursor.fetchall()
            for row in rows:
                print("id = ", row[0])
                print("name = ", row[1], "\n")
        except psycopg2.ProgrammingError as e:
            print(e)
            print("select failed")
        else:
            print("Operation done successfully")
            cursor.close()
     
     
    if __name__ == '__main__':
        try:
            conn = psycopg2.connect(host='10.154.70.231',
                                    port='8000',
                                    database='gaussdb',  # 需要连接的database
                                    user='dbadmin',
                                    password='password')  # 数据库用户密码
        except psycopg2.DatabaseError as ex:
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

    psycopg2接口不提供重试连接的能力，您需要在业务代码中实现重试处理。

    ```
            conn = psycopg2.connect(host='10.154.70.231',
                                    port='8000',
                                    database='gaussdb',  # 需要连接的database
                                    user='dbadmin',
                                    password='password')  # 数据库用户密码
    ```

4.  执行以下命令，使用psycopg第三方库连接集群。

    ```
    python python_dws.py
    ```


## 在Windows环境使用psycopg2第三方库连接集群<a name="section79862501183"></a>

1.  在Windows系统中，单击“开始“按钮 ，在搜索框中，键入**cmd**，然后在结果列表中单击“cmd.exe”打开命令提示符窗口。
2.  在命令提示符窗口中，执行以下命令创建python\_dws.py文件。

    ```
    type nul> python_dws.py
    ```

    请复制粘贴以下内容放入python\_dws.py文件中：

    ```
    #!/usr/bin/python
    # -*- coding:UTF-8 -*-
    
    from __future__ import print_function
    
    import psycopg2
    
    
    def create_table(connection):
        print("Begin to create table")
        try:
            cursor = connection.cursor()
            cursor.execute("drop table if exists test;"
                           "create table test(id int, name text);")
            connection.commit()
        except psycopg2.ProgrammingError as e:
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
        except psycopg2.ProgrammingError as e:
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
            cursor.execute("select * from test order by 1;")
            rows = cursor.fetchall()
            for row in rows:
                print("id = ", row[0])
                print("name = ", row[1], "\n")
        except psycopg2.ProgrammingError as e:
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
            cursor.execute("select * from test order by 1;")
            rows = cursor.fetchall()
            for row in rows:
                print("id = ", row[0])
                print("name = ", row[1], "\n")
        except psycopg2.ProgrammingError as e:
            print(e)
        else:
            print("After Delete,Operation done successfully")
    
    
    def select_data(connection):
        print("Begin to select data")
        try:
            cursor = connection.cursor()
            cursor.execute("select * from test order by 1;")
            rows = cursor.fetchall()
            for row in rows:
                print("id = ", row[0])
                print("name = ", row[1], "\n")
        except psycopg2.ProgrammingError as e:
            print(e)
            print("select failed")
        else:
            print("Operation done successfully")
            cursor.close()
    
    
    if __name__ == '__main__':
        try:
            conn = psycopg2.connect(host='10.154.70.231',
                                    port='8000',
                                    database='postgresgaussdb',  # 需要连接的database
                                    user='dbadmin',
                                    password='password')  # 数据库用户密码
        except psycopg2.DatabaseError as ex:
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

    ```
            conn = psycopg2.connect(host='10.154.70.231',
                                    port='8000',
                                    database='gaussdb',  # 需要连接的database
                                    user='dbadmin',
                                    password='password')  # 数据库用户密码
    ```

4.  在命令提示符窗口中，执行以下命令，使用psycopg第三方库连接集群。

    ```
    python python_dws.py
    ```


## psycopg2连接集群不支持CN Retry特性的问题说明<a name="section9354311165719"></a>

GaussDB\(DWS\)支持在SQL语句执行出错时的自动重试功能（简称CN Retry）。CN Retry对于客户端和驱动发送的SQL语句在执行失败时可以自动识别错误类型，并进行重试，详情请参见[SQL语句出错自动重试](https://support.huaweicloud.com/performance-dws/dws_10_0064.html)。但使用psycopg2默认连接方式创建的连接在语句执行失败时没有自动重试，会直接报错退出。如常见的主备切换场景下，未自动重试会报如下错误，但在自动重试期间完成主备切换，则会返回正确结果。

```
psycopg2.errors.ConnectionFailure: pooler: failed to create 1 connections, Error Message: remote node dn_6003_6004, detail: could not connect to server: Operation now in progress
```

**报错原因：**

1.  psycopg2在发送SQL语句前先发送了BEGIN语句开启事务。
2.  CN Retry不支持事务块中的语句是特性约束。

**解决方案：**

-   在同步方式连接时，可以通过主动结束驱动开启的事务。

    ```
    cursor = conn.cursor()
    # 增加end语句主动结束驱动开启的事务
    cursor.execute("end; select * from test order by 1;") 
    rows = cursor.fetchall()
    ```

-   使用异步连接方式主动开启事务，异步连接介绍具体请参见pyscopg官网：[https://www.psycopg.org/docs/advanced.html?highlight=async](https://www.psycopg.org/docs/advanced.html?highlight=async)。

    ```
    #!/usr/bin/env python3
    # _*_ encoding=utf-8 _*_
     
    import psycopg2
    import select
     
    # psycopg2官方提供的异步连接方式时的wait函数
    # 详见https://www.psycopg.org/docs/advanced.html?highlight=async
    def wait(conn):
        while True:
            state = conn.poll()
            if state == psycopg2.extensions.POLL_OK:
                break
            elif state == psycopg2.extensions.POLL_WRITE:
                select.select([], [conn.fileno()], [])
            elif state == psycopg2.extensions.POLL_READ:
                select.select([conn.fileno()], [], [])
            else:
                raise psycopg2.OperationalError("poll() returned %s" % state)
     
    def psycopg2_cnretry_sync():
        # 创建连接
        conn = psycopg2.connect(host='10.154.70.231',
                                    port='8000',
                                    database='gaussdb',  # 需要连接的database
                                    user='dbadmin',
                                    password='password',  # 数据库用户密码
                                    async=1) # 使用异步方式连接
        wait(conn)
     
        # 执行查询
        cursor = conn.cursor()
        cursor.execute("select * from test order by 1;")
        wait(conn)
        rows = cursor.fetchall()
        for row in rows:
            print(row[0], row[1])
     
        # 关闭连接
        conn.close()
     
    if __name__ == '__main__':
        psycopg2_cnretry_async()
    ```


