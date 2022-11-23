# 配置JDBC连接集群（使用IAM认证方式）<a name="ZH-CN_TOPIC_0000001455917097"></a>

## 概述<a name="section27045914118"></a>

GaussDB\(DWS\) 提供了使用IAM认证方式访问数据库的功能。当使用JDBC应用程序连接集群时，您可以在JDBC连接中配置IAM用户名及其用户凭证等信息，在连接数据库时系统就会自动生成临时数据库凭证，从而成功连接到数据库。

>![](public_sys-resources/icon-note.gif) **说明：** 
>-   当前仅支持1.3.1及以上版本的集群及其配套的JDBC驱动程序使用IAM认证方式访问数据库。请先参考[下载JDBC或ODBC驱动](下载JDBC或ODBC驱动.md)下载JDBC驱动程序。
>-   IoT数仓暂不支持IAM认证方式连接集群。

IAM用户凭证有密码和访问密钥（Access Key ID和Secret Access Key，简称AK和SK）两种类型，您要为JDBC连接提供 IAM 访问密钥。

如需使用IAM用户凭证访问数据库，必须先给您的IAM用户授予DWS Database Access权限，同时拥有DWS  Administrator和DWS  Database Access权限的用户，才能基于IAM用户生成临时数据库用户凭证以连接GaussDB\(DWS\) 数据库。

需要注意的是，DWS Database Access是用户组级别的权限，您可以通过为用户组授权并将用户加入到用户组的方式，使用户具有用户组中的权限。

在IAM中，只有admin用户组的用户可以管理用户。如需给IAM用户授权，您的IAM帐号必须属于IAM的admin用户组，否则，请联系IAM账号管理员帮您授权。

使用IAM用户凭证访问数据库的流程如下：

1.  [授予IAM用户DWS Database Access权限](#section1560842714)
2.  [创建IAM用户凭证](#section5410134511612)
3.  [配置JDBC连接使用IAM认证方式连接集群](#section289114226329)

## 授予IAM用户DWS Database Access权限<a name="section1560842714"></a>

1.  登录华为云管理控制台，单击“服务列表 \> 管理与监管 \> 统一身份认证服务“，打开IAM管理控制台。
2.  修改您的IAM用户所属的用户组，给用户组设置策略，授予用户组DWS Database Access权限，并将您的IAM用户添加到该IAM用户组中。

    只有IAM的admin用户组的用户才能执行此步骤。在IAM中，只有admin用户组的用户可以管理用户，包括创建用户组及用户、设置用户组权限等。

    具体操作请参见《统一身份认证服务用户指南》中的[查看或修改用户组](https://support.huaweicloud.com/usermanual-iam/iam_03_0003.html)。

    您也可以新创建一个IAM用户组，并给用户组设置策略，授予用户组DWS Administrator和DWS Database Access权限，然后将您的IAM用户添加到该IAM用户组中。具体操作请参见《统一身份认证服务用户指南》中的[创建用户组并授权](https://support.huaweicloud.com/usermanual-iam/iam_03_0001.html)。


## 创建IAM用户凭证<a name="section5410134511612"></a>

用户可以登录管理控制台创建访问密钥，如果您已经创建过了，也可以使用已有的访问密钥。

1.  登录管理控制台。
2.  将鼠标移到右上角的用户名，单击“我的凭证”。
3.  再单击“管理访问密钥”页签，可以查看已有的访问密钥，也可以单击“新增访问密钥”进行创建。

    访问密钥是IAM身份认证的重要凭证，只有在新增访问密钥时，用户才可以下载到含有Access Key ID（AK）和Secret Access Key（SK）的密钥文件，在管理控制台只能查看到Access Key ID，如果您未曾下载过该密钥文件，请联系您的管理员进行获取，或者重新创建。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >每个用户最多可创建2个访问密钥，有效期为永久。为了帐号安全性，建议您定期更换并妥善保存访问密钥。


## 配置JDBC连接使用IAM认证方式连接集群<a name="section289114226329"></a>

**配置JDBC连接参数**

**表 1**  数据库连接参数

<a name="table9888102218320"></a>
<table><thead align="left"><tr id="row14882142213212"><th class="cellrowborder" valign="top" width="13%" id="mcps1.2.3.1.1"><p id="p588132273212"><a name="p588132273212"></a><a name="p588132273212"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="87%" id="mcps1.2.3.1.2"><p id="p9881152213326"><a name="p9881152213326"></a><a name="p9881152213326"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row888682211328"><td class="cellrowborder" valign="top" width="13%" headers="mcps1.2.3.1.1 "><p id="p0882132214322"><a name="p0882132214322"></a><a name="p0882132214322"></a>url</p>
</td>
<td class="cellrowborder" valign="top" width="87%" headers="mcps1.2.3.1.2 "><p id="p488217221326"><a name="p488217221326"></a><a name="p488217221326"></a>gsjdbc4.jar/gsjdbc200.jar数据库连接描述符。JDBC接口不提供重试连接的能力，您需要在业务代码中实现重试连接的处理。url示例如下：</p>
<pre class="screen" id="screen1288314225322"><a name="screen1288314225322"></a><a name="screen1288314225322"></a>jdbc:dws:iam://dws-IAM-demo:cn-north-4/<span id="text18822220325"><a name="text18822220325"></a><a name="text18822220325"></a>gaussdb</span>?<strong id="b2882522113215"><a name="b2882522113215"></a><a name="b2882522113215"></a>AccessKeyID</strong>=XXXXXXXXXXXXXXXXXXXX&amp;<strong id="b2882162223211"><a name="b2882162223211"></a><a name="b2882162223211"></a>SecretAccessKey</strong>=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX&amp;<strong id="b18882112283220"><a name="b18882112283220"></a><a name="b18882112283220"></a>DbUser</strong>=user_test&amp;<strong id="b16882322163219"><a name="b16882322163219"></a><a name="b16882322163219"></a>AutoCreate</strong>=true</pre>
<p id="p1788312213328"><a name="p1788312213328"></a><a name="p1788312213328"></a><strong id="b988310228326"><a name="b988310228326"></a><a name="b988310228326"></a>JDBC URL参数说明：</strong></p>
<a name="ul188602215329"></a><a name="ul188602215329"></a><ul id="ul188602215329"><li>jdbc:dws:iam是URL格式的前缀。</li><li>dws-IAM-demo为数据库集群名称。</li><li>cn-north-4是集群所在的区域。<p id="p28845223325"><a name="p28845223325"></a><a name="p28845223325"></a>有关GaussDB(DWS) 的区域信息，请参考<a href="https://developer.huaweicloud.com/endpoint" target="_blank" rel="noopener noreferrer">地区和终端节点</a>。</p>
</li><li><span id="text17884102293217"><a name="text17884102293217"></a><a name="text17884102293217"></a>gaussdb</span>是要连接的数据库名。</li><li>AccessKeyID/SecretAccessKey为参数DbUser指定的IAM用户所对应的访问密钥ID和秘密访问密钥。</li><li>DbUser请设置为IAM用户名，注意，当前版本暂不支持IAM用户名中含有中划线的情况。<a name="ul9885182217324"></a><a name="ul9885182217324"></a><ul id="ul9885182217324"><li>如果数据库中已存在DbUser指定的用户，则临时用户凭证具有与现有用户相同的权限。</li><li>如果数据库中不存在DbUser指定的用户，且AutoCreate参数值为true，则自动创建一个以DbUser参数值作为用户名的新用户，默认创建的用户为数据库普通用户。</li></ul>
</li><li>AutoCreate可以不设置，默认为false。该参数表示是否在数据库中自动创建一个以DbUser参数值作为用户名的数据库用户。<a name="ul1388520223323"></a><a name="ul1388520223323"></a><ul id="ul1388520223323"><li>true表示自动创建。如果用户已存在则不会再创建。</li><li>false表示不会自动创建。如果数据库中不存在DbUser指定的用户名将返回失败。</li></ul>
</li></ul>
</td>
</tr>
<tr id="row1988811222323"><td class="cellrowborder" valign="top" width="13%" headers="mcps1.2.3.1.1 "><p id="p138861722103213"><a name="p138861722103213"></a><a name="p138861722103213"></a>info</p>
</td>
<td class="cellrowborder" valign="top" width="87%" headers="mcps1.2.3.1.2 "><p id="p98861622193217"><a name="p98861622193217"></a><a name="p98861622193217"></a>数据库连接属性。常用的属性如下：</p>
<a name="ul1588812225326"></a><a name="ul1588812225326"></a><ul id="ul1588812225326"><li>ssl：Boolean类型。表示是否使用SSL连接。</li><li>loglevel：Integer类型。为LogStream或LogWriter设置记录进DriverManager当前值的日志信息量。<p id="p388616229321"><a name="p388616229321"></a><a name="p388616229321"></a>目前支持org.postgresql.Driver.DEBUG和org.postgresql.Driver.INFO。值为1时，表示只打印org.postgresql.Driver.INFO，将记录非常少的信息。值大于等于2时，表示打印org.postgresql.Driver.DEBUG和org.postgresql.Driver.INFO，将产生详细的日志信息。默认值为0，表示不打印日志。</p>
</li><li>charSet：String类型。表示在向数据库发送数据或从数据库接收数据时使用到的字符集。</li><li>prepareThreshold：Integer类型。用于确定在转换为服务器端的预备语句之前，要求执行方法PreparedStatement的次数。缺省值是5。</li></ul>
</td>
</tr>
</tbody>
</table>

**示例**

```
//以下用例以gsjdbc4.jar为例。
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

