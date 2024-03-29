# 配置JDBC连接使用IAM认证方式连接集群<a name="ZH-CN_TOPIC_0000001098816702"></a>

当使用JDBC应用程序连接集群时，您可以在JDBC连接中配置IAM用户名及其用户凭证等信息，在连接数据库时系统就会自动生成临时数据库凭证，从而成功连接到数据库。

>![](public_sys-resources/icon-note.gif) **说明：** 
>当前只支持GaussDB\(DWS\)  1.3.1以上版本（包括1.3.1版本）的集群及其配套的JDBC驱动程序使用IAM认证方式访问数据库。请先参考[下载JDBC或ODBC驱动](下载JDBC或ODBC驱动.md)下载JDBC驱动程序。

## 配置JDBC连接参数<a name="section660621017949"></a>

**表 1**  数据库连接参数

<a name="table18711649194147"></a>
<table><thead align="left"><tr id="row49861304194147"><th class="cellrowborder" valign="top" width="13%" id="mcps1.2.3.1.1"><p id="p32179157194147"><a name="p32179157194147"></a><a name="p32179157194147"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="87%" id="mcps1.2.3.1.2"><p id="p37754612194147"><a name="p37754612194147"></a><a name="p37754612194147"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row35428286194147"><td class="cellrowborder" valign="top" width="13%" headers="mcps1.2.3.1.1 "><p id="p23266394194147"><a name="p23266394194147"></a><a name="p23266394194147"></a>url</p>
</td>
<td class="cellrowborder" valign="top" width="87%" headers="mcps1.2.3.1.2 "><p id="p21919088194147"><a name="p21919088194147"></a><a name="p21919088194147"></a>gsjdbc4.jar/gsjdbc200.jar数据库连接描述符。JDBC接口不提供重试连接的能力，您需要在业务代码中实现重试连接的处理。url示例如下：</p>
<pre class="screen" id="screen141022042351"><a name="screen141022042351"></a><a name="screen141022042351"></a>jdbc:dws:iam://dws-IAM-demo:cn-north-4/<span id="text16633144012504"><a name="text16633144012504"></a><a name="text16633144012504"></a>gaussdb</span>?<strong id="b5483181965"><a name="b5483181965"></a><a name="b5483181965"></a>AccessKeyID</strong>=XXXXXXXXXXXXXXXXXXXX&amp;<strong id="b341214711614"><a name="b341214711614"></a><a name="b341214711614"></a>SecretAccessKey</strong>=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX&amp;<strong id="b2226121916612"><a name="b2226121916612"></a><a name="b2226121916612"></a>DbUser</strong>=user_test&amp;<strong id="b57674132619"><a name="b57674132619"></a><a name="b57674132619"></a>AutoCreate</strong>=true</pre>
<p id="p16953174613617"><a name="p16953174613617"></a><a name="p16953174613617"></a><strong id="b72051438995"><a name="b72051438995"></a><a name="b72051438995"></a>JDBC URL参数说明：</strong></p>
<a name="ul7606351173"></a><a name="ul7606351173"></a><ul id="ul7606351173"><li>jdbc:dws:iam是URL格式的前缀。</li><li>dws-IAM-demo为数据库集群名称。</li><li>cn-north-4是集群所在的区域。<p id="p186020359717"><a name="p186020359717"></a><a name="p186020359717"></a>有关GaussDB(DWS) 的区域信息，请参考<a href="https://developer.huaweicloud.com/endpoint" target="_blank" rel="noopener noreferrer">地区和终端节点</a>。</p>
</li><li><span id="text1886587504"><a name="text1886587504"></a><a name="text1886587504"></a>gaussdb</span>是要连接的数据库名。</li><li>AccessKeyID/SecretAccessKey为参数DbUser指定的IAM用户所对应的访问密钥ID和秘密访问密钥。</li><li>DbUser请设置为IAM用户名，注意，当前版本暂不支持IAM用户名中含有中划线的情况。<a name="ul116012358717"></a><a name="ul116012358717"></a><ul id="ul116012358717"><li>如果数据库中已存在DbUser指定的用户，则临时用户凭证具有与现有用户相同的权限。</li><li>如果数据库中不存在DbUser指定的用户，且AutoCreate参数值为true，则自动创建一个以DbUser参数值作为用户名的新用户，默认创建的用户为数据库普通用户。</li></ul>
</li><li>AutoCreate可以不设置，默认为false。该参数表示是否在数据库中自动创建一个以DbUser参数值作为用户名的数据库用户。<a name="ul761335979"></a><a name="ul761335979"></a><ul id="ul761335979"><li>true表示自动创建。如果用户已存在则不会再创建。</li><li>false表示不会自动创建。如果数据库中不存在DbUser指定的用户名将返回失败。</li></ul>
</li></ul>
</td>
</tr>
<tr id="row39648088194147"><td class="cellrowborder" valign="top" width="13%" headers="mcps1.2.3.1.1 "><p id="p40139830194147"><a name="p40139830194147"></a><a name="p40139830194147"></a>info</p>
</td>
<td class="cellrowborder" valign="top" width="87%" headers="mcps1.2.3.1.2 "><p id="p25787388194147"><a name="p25787388194147"></a><a name="p25787388194147"></a>数据库连接属性。常用的属性如下：</p>
<a name="ul23321221194147"></a><a name="ul23321221194147"></a><ul id="ul23321221194147"><li>ssl：Boolean类型。表示是否使用SSL连接。</li><li>loglevel：Integer类型。为LogStream或LogWriter设置记录进DriverManager当前值的日志信息量。<p id="p3597914194147"><a name="p3597914194147"></a><a name="p3597914194147"></a>目前支持org.postgresql.Driver.DEBUG和org.postgresql.Driver.INFO。值为1时，表示只打印org.postgresql.Driver.INFO，将记录非常少的信息。值大于等于2时，表示打印org.postgresql.Driver.DEBUG和org.postgresql.Driver.INFO，将产生详细的日志信息。默认值为0，表示不打印日志。</p>
</li><li>charSet：String类型。表示在向数据库发送数据或从数据库接收数据时使用到的字符集。</li><li>prepareThreshold：Integer类型。用于确定在转换为服务器端的预备语句之前，要求执行方法PreparedStatement的次数。缺省值是5。</li></ul>
</td>
</tr>
</tbody>
</table>

## 示例<a name="section50467166194735"></a>

```
//以下用例以gsjdbc4.jar为例
//以下代码将获取数据库连接操作封装为一个接口，可通过给定集群所在的区域、集群名称、AccessKeyID、SecretAccessKey及对应的IAM用户名来连接数据库。
public static Connection GetConnection(String clustername, String regionname, String AK, String SK, String username) 
    {
        //驱动类。
        String driver = "org.postgresql.Driver";
        //数据库连接描述符。
        String sourceURL = "jdbc:dws:iam://" + clustername + ":" + regionname + "/gaussdb?" + "AccessKeyID=" + AK + "&SecretAccessKey=" + SK + "&DbUser=" + username + "&autoCreate=true";
        
        Connection conn = null;
        
        try
        {
            //加载驱动。
            Class.forName(driver);
        }
        catch( Exception e )
        {
             return null;
        }
        
        try
        {
            //创建连接。
            conn = DriverManager.getConnection(sourceURL);
            System.out.println("Connection succeed!");
         }
        catch(Exception e)
        {
             return null;
        }
        
        return conn;
    };
```

