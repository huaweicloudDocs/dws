# 创建用户并授权使用GaussDB\(DWS\)<a name="ZH-CN_TOPIC_0000001405636790"></a>

如果您需要对您所拥有的GaussDB\(DWS\) 进行精细的权限管理，您可以使用[统一身份认证服务](https://support.huaweicloud.com/usermanual-iam/iam_01_0001.html)（Identity and Access Management，简称IAM）。通过IAM，您可以：

-   根据企业的业务组织，在您的华为云帐号中，给企业中不同职能部门的员工创建IAM用户，让员工拥有唯一安全凭证，并使用GaussDB\(DWS\) 资源。
-   根据企业用户的职能，设置不同的访问权限，以达到用户之间的权限隔离。
-   将GaussDB\(DWS\) 资源委托给更专业、高效的其他华为云帐号或者云服务，这些帐号或者云服务可以根据权限进行代运维。

如果华为云帐号已经能满足您的要求，不需要创建独立的IAM用户，您可以跳过本章节，不影响您使用GaussDB\(DWS\) 服务的其它功能。

本章节为您介绍对用户授权的方法，操作流程如[示例流程](#section9135134520119)所示。

## 前提条件<a name="section149106163317"></a>

给用户组授权之前，请您了解用户组可以添加的GaussDB\(DWS\) 权限，并结合实际需求进行选择，GaussDB\(DWS\) 支持的系统权限，请参见：[GaussDB\(DWS\)系统权限](https://support.huaweicloud.com/productdesc-dws/dws_01_0144.html)。若您需要对除GaussDB\(DWS\) 之外的其它服务授权，IAM支持服务的所有权限请参见[系统权限](https://support.huaweicloud.com/usermanual-permissions/iam_01_0001.html)。

## 示例流程<a name="section9135134520119"></a>

**图 1**  给用户授权GaussDB\(DWS\) 权限流程<a name="fig1014814451016"></a>  
![](figures/给用户授权GaussDB(DWS)-权限流程.png "给用户授权GaussDB(DWS)-权限流程")

1.  <a name="li863810121421"></a>[创建用户组并授权](https://support.huaweicloud.com/usermanual-iam/iam_03_0001.html)

    使用华为云帐号登录[IAM控制台](https://console.huaweicloud.com/iam)，创建用户组，并授予数据仓库服务的只读权限“DWS ReadOnlyAccess“。

2.  [创建用户并加入用户组](https://support.huaweicloud.com/usermanual-iam/iam_02_0001.html)

    在IAM控制台创建用户，并将其加入步骤[1](#li863810121421)中创建的用户组。

3.  [用户登录](https://support.huaweicloud.com/usermanual-iam/iam_01_0552.html)并验证权限

    使用新创建的用户登录控制台，切换至授权区域，验证权限：

    -   在“服务列表”中选择数据仓库服务，进入DWS主界面，单击右上角“创建数据仓库集群“，尝试创建数据仓库集群，如果无法创建（假设当前权限仅包含DWS ReadOnlyAccess），表示“DWS ReadOnlyAccess“已生效。
    -   在“服务列表”中选择除数据仓库服务之外（假设当前策略仅包含DWS ReadOnlyAccess）的任一服务，若提示权限不足，表示“DWS ReadOnlyAccess“已生效。


