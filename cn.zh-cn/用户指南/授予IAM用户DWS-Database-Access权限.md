# 授予IAM用户DWS Database Access权限<a name="dws_01_0135"></a>

如需使用IAM用户凭证访问数据库，必须先给您的IAM用户授予DWS Database Access权限，拥有该权限的用户，才能基于IAM用户生成临时数据库用户凭证以连接DWS数据库。通过DWS Database Access权限的授权和限制，用户可以更好地管理数据库的访问权限。

需要注意的是，DWS Database Access是用户组级别的权限，您可以通过为用户组授权并将用户加入到用户组的方式，使用户具有用户组中的权限。

在IAM中，只有admin用户组的用户可以管理用户。如需给IAM用户授权，您的IAM账号必须属于IAM的admin用户组，否则，请联系管理员帮您授权。

## 授予IAM用户DWS Database Access权限<a name="section183185863313"></a>

给IAM用户授权，首先要登录IAM管理控制台。然后必须先给一个IAM用户组（可以新建一个用户组）授予DWS Database Access权限，再将您的IAM用户添加到该IAM用户组中，如此，该IAM用户就获得了DWS Database Access权限。IAM的相关操作请参考《统一身份认证服务用户指南》。

