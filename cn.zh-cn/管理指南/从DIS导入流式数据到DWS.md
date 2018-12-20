# 从DIS导入流式数据到DWS<a name="dws_01_0115"></a>

通过数据接入服务（Data Ingestion Service，简称DIS），可以将实时数据从DIS导入到DWS集群的数据库中。在这种场景下，DIS通道里的流式数据存储在DIS中，并周期性导入DWS中。导入DWS前数据临时存储在OBS，待转储DWS完成后删除OBS上的临时存储数据。

从DIS导入数据到DWS的流程如下：

1.  [创建DWS集群、数据库和数据表](#section1127881012522)
2.  [开通DIS通道，接入实时数据](#section67561112547)
3.  [在DWS数据库中查看从DIS导入的数据](#section17542621535)

## 创建DWS集群、数据库和数据表<a name="section1127881012522"></a>

1.  创建DWS集群。

    详细的操作步骤，请参见[创建集群](创建集群.md)。如果您已经有DWS集群了，也可以跳过这一步。

    例如，创建一个名为"dws-demo"的DWS集群。

2.  使用SQL客户端连接DWS集群。

    有关使用SQL客户端连接DWS集群的操作，请参见[连接集群](连接集群.md)，您可以选择其中一种方式连接集群。

3.  在SQL客户端中，执行SQL语句，创建数据库、数据表和数据库模式（即schema）。

    请参见《数据仓库服务数据库开发指南》的[从这里开始](https://support.huaweicloud.com/devg-dws/before_you_start_0001.md)  ，完成如下数据库对象的创建：

    -   数据库用户：用户名为“joe”， 密码为“Bigdata@123”。
    -   数据库：“db\_tpcds”。
    -   数据库模式：“myschema”。

        如果您选择不创建数据库模式，默认情况下，新的数据库对象是创建在“public”模式下的。

    -   数据表：“mytable”。

        创建数据表时，请根据实际的源数据设计表结构。表的字段及其字段类型要和源数据一一对应。



## 开通DIS通道，接入实时数据<a name="section67561112547"></a>

1.  在开通DIS通道前，先申请一个用于数据临时转储缓存的OBS桶。

    有关申请OBS桶的详细操作，请参见《对象存储服务控制台指南》的“入门”。如果您已经有OBS桶了，也可以跳过这一步。

    例如，创建了一个名为“obs-dis-input”的OBS桶，并在桶内新建了一个文件夹“input\_data”。

2.  开通DIS通道。

    开通DIS通道的步骤大致如下，更多信息，请参见《数据接入服务用户指南》的[开通DIS通道](https://support.huaweicloud.com/usermanual-dis/zh-cn_topic_0034903799.html)章节。

    1.  登录DIS管理控制台。
    2.  单击“申请接入通道”，进入“申请接入通道”页面，您可以参考下列表格配置相关参数。

        **表 1**  地域

        <a name="table59125155411"></a>
        <table><thead align="left"><tr id="row591165155417"><th class="cellrowborder" valign="top" width="17.169999999999998%" id="mcps1.2.4.1.1"><p id="p691185118549"><a name="p691185118549"></a><a name="p691185118549"></a>参数</p>
        </th>
        <th class="cellrowborder" valign="top" width="60.209999999999994%" id="mcps1.2.4.1.2"><p id="p891251105414"><a name="p891251105414"></a><a name="p891251105414"></a>参数说明</p>
        </th>
        <th class="cellrowborder" valign="top" width="22.62%" id="mcps1.2.4.1.3"><p id="p1491751145413"><a name="p1491751145413"></a><a name="p1491751145413"></a>样例值</p>
        </th>
        </tr>
        </thead>
        <tbody><tr id="row189135105412"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p591115116546"><a name="p591115116546"></a><a name="p591115116546"></a>当前区域</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><p id="p591165105416"><a name="p591165105416"></a><a name="p591165105416"></a>选择与DWS集群相同的区域。您可以在页面左上角切换区域。</p>
        <div class="note" id="note995125125412"><a name="note995125125412"></a><a name="note995125125412"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p595115114548"><a name="p595115114548"></a><a name="p595115114548"></a>目前区域仅支持<strong id="b159505115542"><a name="b159505115542"></a><a name="b159505115542"></a>华北</strong>。</p>
        </div></div>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p15911651145414"><a name="p15911651145414"></a><a name="p15911651145414"></a>华北-北京一</p>
        </td>
        </tr>
        </tbody>
        </table>

        **表 2**  基本信息

        <a name="table794125117547"></a>
        <table><thead align="left"><tr id="row189195112541"><th class="cellrowborder" valign="top" width="17.169999999999998%" id="mcps1.2.4.1.1"><p id="p1791051125418"><a name="p1791051125418"></a><a name="p1791051125418"></a>参数</p>
        </th>
        <th class="cellrowborder" valign="top" width="60.209999999999994%" id="mcps1.2.4.1.2"><p id="p12911517546"><a name="p12911517546"></a><a name="p12911517546"></a>参数说明</p>
        </th>
        <th class="cellrowborder" valign="top" width="22.62%" id="mcps1.2.4.1.3"><p id="p49125113545"><a name="p49125113545"></a><a name="p49125113545"></a>样例值</p>
        </th>
        </tr>
        </thead>
        <tbody><tr id="row691195105412"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p169113515542"><a name="p169113515542"></a><a name="p169113515542"></a>通道名称</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><p id="p591851145418"><a name="p591851145418"></a><a name="p591851145418"></a>DIS通道名称。</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p19116515544"><a name="p19116515544"></a><a name="p19116515544"></a>dis-input</p>
        </td>
        </tr>
        <tr id="row69275105418"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p1991351105419"><a name="p1991351105419"></a><a name="p1991351105419"></a>通道类型</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><a name="ul59117519540"></a><a name="ul59117519540"></a><ul id="ul59117519540"><li>普通通道：最高发送速度可达1MB/秒及1000条记录/秒，最高提取速度可达2MB/秒。</li><li>高级通道：最高发送速度可达5MB/秒及2000条记录/秒，最高提取速度可达10MB/秒。</li></ul>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p892155114544"><a name="p892155114544"></a><a name="p892155114544"></a>普通通道</p>
        </td>
        </tr>
        <tr id="row19216519542"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p1992105185416"><a name="p1992105185416"></a><a name="p1992105185416"></a>分区数量</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><p id="p1992165117546"><a name="p1992165117546"></a><a name="p1992165117546"></a>分区是DIS数据通道的基本吞吐量单位。</p>
        <p id="p101756513418"><a name="p101756513418"></a><a name="p101756513418"></a>用户可以手动输入一个值，也可以单击“分区计算”，在弹出的对话框中，根据实际需求设置，通过系统计算得到一个建议的分区数量值。</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p1992151115415"><a name="p1992151115415"></a><a name="p1992151115415"></a>2</p>
        </td>
        </tr>
        <tr id="row194105120544"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p892185119541"><a name="p892185119541"></a><a name="p892185119541"></a>源数据类型</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><p id="p79265145417"><a name="p79265145417"></a><a name="p79265145417"></a>从DIS导入数据到DWS的场景，<span class="parmname" id="parmname159214513547"><a name="parmname159214513547"></a><a name="parmname159214513547"></a>“源数据类型”</span>只支持<span class="parmvalue" id="parmvalue209295118549"><a name="parmvalue209295118549"></a><a name="parmvalue209295118549"></a>“BLOB”</span>，<span class="parmvalue" id="parmvalue09225115418"><a name="parmvalue09225115418"></a><a name="parmvalue09225115418"></a>“BLOB”</span>表示二进制数据。</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p592205145414"><a name="p592205145414"></a><a name="p592205145414"></a>BLOB</p>
        </td>
        </tr>
        <tr id="row394135145417"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p094851195411"><a name="p094851195411"></a><a name="p094851195411"></a>生命周期（天）</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><p id="p594105155412"><a name="p594105155412"></a><a name="p594105155412"></a>存储在DIS中的数据保留的最长时间，超过此时长数据将被清除。</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p129416516544"><a name="p129416516544"></a><a name="p129416516544"></a>1</p>
        </td>
        </tr>
        </tbody>
        </table>

        以下[表3](#table1100051175411)中的参数，请根据[创建DWS集群、数据库和数据表](#section1127881012522)中的情况进行填写。

        **表 3**  “数据转储”相关参数

        <a name="table1100051175411"></a>
        <table><thead align="left"><tr id="row69412518544"><th class="cellrowborder" valign="top" width="17.169999999999998%" id="mcps1.2.4.1.1"><p id="p199445118546"><a name="p199445118546"></a><a name="p199445118546"></a>参数</p>
        </th>
        <th class="cellrowborder" valign="top" width="60.209999999999994%" id="mcps1.2.4.1.2"><p id="p1594251175415"><a name="p1594251175415"></a><a name="p1594251175415"></a>参数说明</p>
        </th>
        <th class="cellrowborder" valign="top" width="22.62%" id="mcps1.2.4.1.3"><p id="p1094351205412"><a name="p1094351205412"></a><a name="p1094351205412"></a>样例值</p>
        </th>
        </tr>
        </thead>
        <tbody><tr id="row1951351195418"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p1194951115419"><a name="p1194951115419"></a><a name="p1194951115419"></a>转储开关</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><p id="p1094205117540"><a name="p1094205117540"></a><a name="p1094205117540"></a>设置为开启，开启后通道数据转储至指定的<span class="parmname" id="parmname09515115413"><a name="parmname09515115413"></a><a name="parmname09515115413"></a>“转储服务类型”</span>中。</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p49525117542"><a name="p49525117542"></a><a name="p49525117542"></a><a name="image769854625910"></a><a name="image769854625910"></a><span><img id="image769854625910" src="figures/icon_dws_on.png"></span></p>
        </td>
        </tr>
        <tr id="row79611517548"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p149512518545"><a name="p149512518545"></a><a name="p149512518545"></a>转储服务类型</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><p id="p080672911104"><a name="p080672911104"></a><a name="p080672911104"></a>选择<span class="parmvalue" id="parmvalue1480642913101"><a name="parmvalue1480642913101"></a><a name="parmvalue1480642913101"></a>“DWS”</span>。</p>
        <p id="p16572113416916"><a name="p16572113416916"></a><a name="p16572113416916"></a>通道里的流式数据存储在DIS中，并周期性导入DWS中。导入DWS前数据临时存储在OBS，待转储DWS完成后删除OBS上的临时存储数据。</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p3965516549"><a name="p3965516549"></a><a name="p3965516549"></a>DWS</p>
        </td>
        </tr>
        <tr id="row1696155185411"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p396195175410"><a name="p396195175410"></a><a name="p396195175410"></a>DWS 集群</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><p id="p9961251115411"><a name="p9961251115411"></a><a name="p9961251115411"></a>存储该通道数据的DWS集群名称。</p>
        <p id="p10963516549"><a name="p10963516549"></a><a name="p10963516549"></a>单击<span class="uicontrol" id="uicontrol135399591210"><a name="uicontrol135399591210"></a><a name="uicontrol135399591210"></a>“选择”</span>，在弹出的<span class="wintitle" id="wintitle159325316128"><a name="wintitle159325316128"></a><a name="wintitle159325316128"></a>“选择DWS集群”</span>窗口中选择一个DWS集群。</p>
        <p id="p6962051135411"><a name="p6962051135411"></a><a name="p6962051135411"></a>此配置项仅支持选择，不可手动输入。</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p29614516548"><a name="p29614516548"></a><a name="p29614516548"></a>dws-demo</p>
        </td>
        </tr>
        <tr id="row199611516546"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p209675113540"><a name="p209675113540"></a><a name="p209675113540"></a>DWS 数据库</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><p id="p596135135415"><a name="p596135135415"></a><a name="p596135135415"></a>存储该通道数据的DWS数据库名称。</p>
        <p id="p096185118544"><a name="p096185118544"></a><a name="p096185118544"></a>手动输入，不可配置为空。</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p1996175120541"><a name="p1996175120541"></a><a name="p1996175120541"></a>db_tpcds</p>
        </td>
        </tr>
        <tr id="row497155165413"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p996151145410"><a name="p996151145410"></a><a name="p996151145410"></a>数据库模式</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><p id="p1796751185413"><a name="p1796751185413"></a><a name="p1796751185413"></a>存储该通道数据的DWS数据库模式（即schema）。</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p5976511540"><a name="p5976511540"></a><a name="p5976511540"></a>myschema</p>
        </td>
        </tr>
        <tr id="row1797155165417"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p179775113547"><a name="p179775113547"></a><a name="p179775113547"></a>DWS 数据表</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><p id="p39795155416"><a name="p39795155416"></a><a name="p39795155416"></a>存储该通道数据的DWS数据库模式下的数据表。</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p10971051155414"><a name="p10971051155414"></a><a name="p10971051155414"></a>mytable</p>
        </td>
        </tr>
        <tr id="row498175155419"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p2971951165417"><a name="p2971951165417"></a><a name="p2971951165417"></a>数据分隔符</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><p id="p097175113543"><a name="p097175113543"></a><a name="p097175113543"></a>用户数据的字段分隔符，根据此分隔符分隔用户数据插入DWS数据表的相应列。</p>
        <p id="p798145115415"><a name="p798145115415"></a><a name="p798145115415"></a>取值范围：<span class="parmvalue" id="parmvalue8988518546"><a name="parmvalue8988518546"></a><a name="parmvalue8988518546"></a>“，”</span>、<span class="parmvalue" id="parmvalue2098165118542"><a name="parmvalue2098165118542"></a><a name="parmvalue2098165118542"></a>“；”</span>和<span class="parmvalue" id="parmvalue14981851145414"><a name="parmvalue14981851145414"></a><a name="parmvalue14981851145414"></a>“|”</span>三种字符中的一个。</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p149895110546"><a name="p149895110546"></a><a name="p149895110546"></a>,</p>
        </td>
        </tr>
        <tr id="row1899451175420"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p1698951195414"><a name="p1698951195414"></a><a name="p1698951195414"></a>数据转储周期（s）</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><p id="p6998519542"><a name="p6998519542"></a><a name="p6998519542"></a>根据用户配置的时间，周期性的将数据导入OBS，若某个时间段内无数据，则此时间段不会生成打包文件。</p>
        <p id="p299195120549"><a name="p299195120549"></a><a name="p299195120549"></a>取值范围：60～900。</p>
        <p id="p149905165415"><a name="p149905165415"></a><a name="p149905165415"></a>单位：秒。</p>
        <p id="p39918516540"><a name="p39918516540"></a><a name="p39918516540"></a>默认配置为300秒。</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p1799951105418"><a name="p1799951105418"></a><a name="p1799951105418"></a>300</p>
        </td>
        </tr>
        <tr id="row18996512543"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p599125125420"><a name="p599125125420"></a><a name="p599125125420"></a>失败重试时效 (s)</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><p id="p1399135115546"><a name="p1399135115546"></a><a name="p1399135115546"></a>用户数据转储失败的重试失效时间。重试时间超过该配置项配置的值，则将转储失败的数据备份至OBS桶对应的目录下。</p>
        <p id="p179917513546"><a name="p179917513546"></a><a name="p179917513546"></a>取值范围：0~7200。</p>
        <p id="p11991351115415"><a name="p11991351115415"></a><a name="p11991351115415"></a>单位：秒。</p>
        <p id="p159965115543"><a name="p159965115543"></a><a name="p159965115543"></a>默认配置为1800。</p>
        <p id="p89935175411"><a name="p89935175411"></a><a name="p89935175411"></a>配置为<span class="parmvalue" id="parmvalue79945135411"><a name="parmvalue79945135411"></a><a name="parmvalue79945135411"></a>“0”</span>表示DIS服务不会在转储失败时进行重试。</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p1099851125415"><a name="p1099851125415"></a><a name="p1099851125415"></a>1800</p>
        </td>
        </tr>
        </tbody>
        </table>

        以下[表4](#table3532131218010)中的参数，请根据[创建DWS集群、数据库和数据表](#section1127881012522)中的情况进行填写。

        **表 4**  “登录”相关参数

        <a name="table3532131218010"></a>
        <table><thead align="left"><tr id="row555411121408"><th class="cellrowborder" valign="top" width="17.169999999999998%" id="mcps1.2.4.1.1"><p id="p755911219015"><a name="p755911219015"></a><a name="p755911219015"></a>参数</p>
        </th>
        <th class="cellrowborder" valign="top" width="60.209999999999994%" id="mcps1.2.4.1.2"><p id="p1156481213010"><a name="p1156481213010"></a><a name="p1156481213010"></a>参数说明</p>
        </th>
        <th class="cellrowborder" valign="top" width="22.62%" id="mcps1.2.4.1.3"><p id="p205678124020"><a name="p205678124020"></a><a name="p205678124020"></a>样例值</p>
        </th>
        </tr>
        </thead>
        <tbody><tr id="row185798121010"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p65829121903"><a name="p65829121903"></a><a name="p65829121903"></a>用户名</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><p id="p658717128013"><a name="p658717128013"></a><a name="p658717128013"></a>DWS集群数据库的用户名。</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p14590131219016"><a name="p14590131219016"></a><a name="p14590131219016"></a>joe</p>
        </td>
        </tr>
        <tr id="row7593141213016"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p125951012300"><a name="p125951012300"></a><a name="p125951012300"></a>密码</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><p id="p13598412302"><a name="p13598412302"></a><a name="p13598412302"></a>DWS集群数据库的密码。</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p360211121403"><a name="p360211121403"></a><a name="p360211121403"></a>Bigdata@123</p>
        </td>
        </tr>
        <tr id="row46025126017"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p260714124013"><a name="p260714124013"></a><a name="p260714124013"></a>KMS密钥</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><p id="p15610112809"><a name="p15610112809"></a><a name="p15610112809"></a>用户在密钥管理服务（KMS）创建的用户密钥名称。</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p1161415128012"><a name="p1161415128012"></a><a name="p1161415128012"></a>-</p>
        </td>
        </tr>
        </tbody>
        </table>

        **表 5**  “转储缓存”和“授权”相关参数

        <a name="table9111135113545"></a>
        <table><thead align="left"><tr id="row81016513547"><th class="cellrowborder" valign="top" width="17.169999999999998%" id="mcps1.2.4.1.1"><p id="p1610117517546"><a name="p1610117517546"></a><a name="p1610117517546"></a>参数</p>
        </th>
        <th class="cellrowborder" valign="top" width="60.209999999999994%" id="mcps1.2.4.1.2"><p id="p8101251145417"><a name="p8101251145417"></a><a name="p8101251145417"></a>参数说明</p>
        </th>
        <th class="cellrowborder" valign="top" width="22.62%" id="mcps1.2.4.1.3"><p id="p6101125185420"><a name="p6101125185420"></a><a name="p6101125185420"></a>样例值</p>
        </th>
        </tr>
        </thead>
        <tbody><tr id="row1510514511546"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p81051651125418"><a name="p81051651125418"></a><a name="p81051651125418"></a>数据临时桶</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><p id="p6105195113544"><a name="p6105195113544"></a><a name="p6105195113544"></a>用户数据会先临时存储在OBS桶中用户配置的临时目录下，再转储到指定的转储服务，转储完成后临时目录中的数据会被清除。</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p101051651145411"><a name="p101051651145411"></a><a name="p101051651145411"></a>obs-dis-input</p>
        </td>
        </tr>
        <tr id="row7106155125418"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p12106195155415"><a name="p12106195155415"></a><a name="p12106195155415"></a>数据临时目录</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><p id="p1910615125416"><a name="p1910615125416"></a><a name="p1910615125416"></a>需要转储的数据临时存储在OBS桶下此配置项配置的目录中，转储完成后临时目录中的数据会被清除。</p>
        <p id="p01061351165411"><a name="p01061351165411"></a><a name="p01061351165411"></a>配置为空时，数据直接存储在OBS桶内。</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p5106125110545"><a name="p5106125110545"></a><a name="p5106125110545"></a>input_data</p>
        </td>
        </tr>
        <tr id="row14106185105412"><td class="cellrowborder" valign="top" width="17.169999999999998%" headers="mcps1.2.4.1.1 "><p id="p1110611510548"><a name="p1110611510548"></a><a name="p1110611510548"></a>IAM 委托</p>
        </td>
        <td class="cellrowborder" valign="top" width="60.209999999999994%" headers="mcps1.2.4.1.2 "><p id="p1106105111547"><a name="p1106105111547"></a><a name="p1106105111547"></a>DIS需要获取IAM 委托信息去访问指定的资源，委托需具有指定资源的操作权限。</p>
        <p id="p191061517540"><a name="p191061517540"></a><a name="p191061517540"></a>此配置项仅支持下拉框选择。</p>
        <p id="p1253622211149"><a name="p1253622211149"></a><a name="p1253622211149"></a>请参见《数据接入服务用户指南》的“IAM中创建DIS委托”章节。</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.62%" headers="mcps1.2.4.1.3 "><p id="p7106751105417"><a name="p7106751105417"></a><a name="p7106751105417"></a>-</p>
        </td>
        </tr>
        </tbody>
        </table>


3.  准备DIS应用开发环境，发送实时数据到DIS。

    详细操作，请参见《数据接入服务用户指南》的“准备DIS应用开发环境”和“发送数据到DIS”章节。


## 在DWS数据库中查看从DIS导入的数据<a name="section17542621535"></a>

1.  使用SQL客户端连接DWS集群中已导入DIS数据的数据库。

    有关使用SQL客户端连接DWS集群的操作，请参见[连接集群](连接集群.md)，您可以选择其中一种方式连接集群。

2.  在SQL客户端中执行查询命令，查看从DIS导入DWS的数据。

    命令示例如下，其中table\_name请替换为在开通DIS通道时[表3](#table1100051175411)中的“DWS 数据表“参数指定的表名。

    ```
    SELECT * FROM table_name;
    ```


