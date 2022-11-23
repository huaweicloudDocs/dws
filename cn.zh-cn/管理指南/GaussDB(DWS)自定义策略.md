# GaussDB\(DWS\)自定义策略<a name="ZH-CN_TOPIC_0000001455716733"></a>

如果系统预置的GaussDB\(DWS\) 权限，不满足您的授权要求，可以创建自定义策略。自定义策略中可以添加的授权项（Action）请参考[权限策略和授权项](策略语法-细粒度策略.md#section447711462541)。

目前华为云支持以下两种方式创建自定义策略：

-   可视化视图创建自定义策略：无需了解策略语法，按可视化视图导航栏选择云服务、操作、资源、条件等策略内容，可自动生成策略。
-   JSON视图创建自定义策略：可以在选择策略模板后，根据具体需求编辑策略内容；也可以直接在编辑框内编写JSON格式的策略内容。

具体创建步骤请参见：[创建自定义策略](https://support.huaweicloud.com/usermanual-iam/iam_01_0605.html)。本章为您介绍常用的GaussDB\(DWS\) 自定义策略样例。

## GaussDB\(DWS\) 自定义策略样例<a name="section1493518251395"></a>

-   示例1：授权用户创建/恢复集群、重启集群、删除集群、设置安全参数、重置密码的权限。

    ```
    {
          "Version": "1.1",
          "Statement": [
                {
                      "Effect": "Allow",
                      "Action": [
                            "dws:cluster:create",
                            "dws:cluster:restart",
                            "dws:cluster:delete",
                            "dws:cluster:setSecuritySettings",
                            "dws:cluster:resetPassword",
                            "ecs:*:get*",
                            "ecs:*:list*",
                            "ecs:*:create*",
                            "ecs:*:delete*",
                            "vpc:*:get*",
                            "vpc:*:list*",
                            "vpc:*:create*",
                            "vpc:*:delete*",
                            "evs:*:get*",
                            "evs:*:list*",
                            "evs:*:create*",
                            "evs:*:delete*"
                      ]
                }
          ]
    }
    ```

-   示例2：通配符\*用法示例

    例如，以下策略具有对GaussDB\(DWS\)快照的所有操作权限。

    ```
    {
          "Version": "1.1",
          "Statement": [
                {
                      "Effect": "Allow",
                      "Action": [
                            "dws:snapshot:*",
                            "ecs:*:get*",
                            "ecs:*:list*",
                            "vpc:*:get*",
                            "vpc:*:list*"
                      ]
                }
          ]
    }
    ```

-   示例3：拒绝用户删除集群

    拒绝策略需要同时配合其他策略使用，否则没有实际作用。用户被授予的策略中，一个授权项的作用如果同时存在Allow和Deny，则遵循**Deny优先原则**。

    如果您给用户授予GaussDB\(DWS\)  FullAccess的系统策略，但不希望用户拥有GaussDB\(DWS\)  FullAccess中定义的删除集群权限，您可以创建一条拒绝删除集群的自定义策略，然后同时将GaussDB\(DWS\)  FullAccess和拒绝策略授予用户，根据Deny优先原则，则用户可以对GaussDB\(DWS\) 执行除了删除集群外的所有操作。拒绝策略示例如下：

    ```
    { 
          "Version": "1.1", 
          "Statement": [ 
                { 
    		  "Effect": "Deny", 
                      "Action": [ 
                            "dws:cluster:delete"
                      ] 
                } 
          ] 
    }
    ```

-   示例4：多个授权项策略

    一个自定义策略中可以包含多个授权项，且除了可以包含本服务的授权项外，还可以包含其他服务的授权项，可以包含的其他服务必须跟本服务同属性，即都是项目级服务或都是全局级服务。多个授权语句策略描述如下：

    ```
    {  
             "Version": "1.1",  
             "Statement": [  
                     {  
                     "Effect": "Allow",
                     "Action": [  
                            "dws:cluster:create",
                            "dws:cluster:restart",
                            "dws:cluster:setSecuritySettings",
                            "dws:*:get*",
                            "dws:*:list*",
                            "ecs:*:get*",
                            "ecs:*:list*",
                            "ecs:*:create*",
                            "vpc:*:get*",
                            "vpc:*:list*",
                            "vpc:*:create*",
                            "evs:*:get*",
                            "evs:*:list*",
                            "evs:*:create*"
                      ]
                     },
                    { 
    		  "Effect": "Deny", 
                      "Action": [ 
                            "dws:cluster:delete"
                      ] 
                    } 
    
             ]  
     }
    ```


