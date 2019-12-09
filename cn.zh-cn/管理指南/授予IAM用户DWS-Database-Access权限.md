# 授予IAM用户DWS Database Access权限<a name="dws_01_0135"></a>

如需使用IAM用户凭证访问数据库，必须先给您的IAM用户授予DWS Database Access权限，同时拥有DWS Administrator和DWS Database Access权限的用户，才能基于IAM用户生成临时数据库用户凭证以连接DWS数据库。通过DWS Database Access权限的授权和限制，用户可以更好地管理数据库的访问权限。

需要注意的是，DWS Database Access是用户组级别的权限，您可以通过为用户组授权并将用户加入到用户组的方式，使用户具有用户组中的权限。

在IAM中，只有admin用户组的用户可以管理用户。如需给IAM用户授权，您的IAM账号必须属于IAM的admin用户组，否则，请联系管理员帮您授权。

## 授予IAM用户DWS Database Access权限<a name="section183185863313"></a>

1.  登录公有云管理控制台，单击“服务列表 \> 管理与部署 \> 统一身份认证服务“，打开IAM管理控制台。
2.  修改您的IAM用户所属的用户组，给用户组设置策略，授予用户组DWS Database Access权限，并将您的IAM用户添加到该IAM用户组中。

    只有IAM的admin用户组的用户才能执行此步骤。在IAM中，只有admin用户组的用户可以管理用户，包括创建用户组及用户、设置用户组权限等。

    具体操作请参见《统一身份认证服务用户指南》中的[查看或修改用户组](https://support.huaweicloud.com/usermanual-iam/zh-cn_topic_0085605493.html)。

    您也可以新创建一个IAM用户组，并给用户组设置策略，授予用户组DWS Administrator和DWS Database Access权限，然后将您的IAM用户添加到该IAM用户组中。具体操作请参见《统一身份认证服务用户指南》中的[创建用户组并授权](https://support.huaweicloud.com/usermanual-iam/zh-cn_topic_0046611269.html)。


