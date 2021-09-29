# GaussDB\(DWS\) 自定义策略<a name="ZH-CN_TOPIC_0000001145496715"></a>

如果系统预置的GaussDB\(DWS\) 权限，不满足您的授权要求，可以创建自定义策略。自定义策略中可以添加的授权项（Action）请参考[权限策略和授权项](#section20504546151912)。

目前公有云支持以下两种方式创建自定义策略：

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
                            "dws:cluster:setParameter",
                            "dws:cluster:resetPassword",
                            "ecs:*:get*",
                            "ecs:*:list*",
                            "vpc:*:get*",
                            "vpc:*:list*"
                      ]
                }
          ]
    }
    ```

-   示例2：拒绝用户删除集群

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

-   示例3：多个授权项策略

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
                            "dws:cluster:setParameter",
                            "dws:*:get*",
                            "dws:*:list*",
                            "ecs:*:get*",
                            "ecs:*:list*",
                            "vpc:*:get*",
                            "vpc:*:list*"
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


## GaussDB\(DWS\) 细粒度策略授权项列表<a name="section20504546151912"></a>

在IAM中创建自定义策略时，您可以根据需求在策略授权语句的Action列表中添加GaussDB\(DWS\) 资源操作或REST API所对应的“授权项”，使得该策略具有相应的操作权限。GaussDB\(DWS\) 细粒度策略的授权项列表如下：

-   **REST API**

    GaussDB\(DWS\)  REST API的授权项列表，请参见[权限策略和授权项](https://support.huaweicloud.com/api-dws/dws_02_0056.html)。

-   **管理控制台操作**

    GaussDB\(DWS\) 资源操作及对应的授权项如[表1](#t37dcc3c5be924910bd9b84d7e8c92d11)所示。


**表 1**  GaussDB\(DWS\) 资源操作授权项列表

<a name="t37dcc3c5be924910bd9b84d7e8c92d11"></a>
<table><thead align="left"><tr id="r5d1f1cfde0d247df8a239793ea7f03d7"><th class="cellrowborder" valign="top" width="22.6%" id="mcps1.2.5.1.1"><p id="a18d6dec9ce954836a9bdcdeb26de523f"><a name="a18d6dec9ce954836a9bdcdeb26de523f"></a><a name="a18d6dec9ce954836a9bdcdeb26de523f"></a>GaussDB(DWS) 资源操作</p>
</th>
<th class="cellrowborder" valign="top" width="31.81%" id="mcps1.2.5.1.2"><p id="adeeca03489fb4cb1bdc5a7e9ff8aa527"><a name="adeeca03489fb4cb1bdc5a7e9ff8aa527"></a><a name="adeeca03489fb4cb1bdc5a7e9ff8aa527"></a>授权项</p>
</th>
<th class="cellrowborder" valign="top" width="26.21%" id="mcps1.2.5.1.3"><p id="aa81ae2ce2df7445bb1b3384ebe3883dc"><a name="aa81ae2ce2df7445bb1b3384ebe3883dc"></a><a name="aa81ae2ce2df7445bb1b3384ebe3883dc"></a>依赖的授权项</p>
</th>
<th class="cellrowborder" valign="top" width="19.38%" id="mcps1.2.5.1.4"><p id="zh-cn_topic_0167929270_p29118351780"><a name="zh-cn_topic_0167929270_p29118351780"></a><a name="zh-cn_topic_0167929270_p29118351780"></a>授权项作用域</p>
</th>
</tr>
</thead>
<tbody><tr id="r8857c9ff9bc44c538d4e4b401d373dac"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="adfe19f67225a464b85dd9376cc65ed79"><a name="adfe19f67225a464b85dd9376cc65ed79"></a><a name="adfe19f67225a464b85dd9376cc65ed79"></a>创建/恢复集群</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0167929270_p251773918465"><a name="zh-cn_topic_0167929270_p251773918465"></a><a name="zh-cn_topic_0167929270_p251773918465"></a>"dws:cluster:create"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="a57959e95290e4a70992a098df94c464f"><a name="a57959e95290e4a70992a098df94c464f"></a><a name="a57959e95290e4a70992a098df94c464f"></a>"dws:*:get*",</p>
<p id="ac8a8d6e4f93249ef9e300c98890f28f2"><a name="ac8a8d6e4f93249ef9e300c98890f28f2"></a><a name="ac8a8d6e4f93249ef9e300c98890f28f2"></a>"dws:*:list*",</p>
<p id="zh-cn_topic_0167929270_p446655811403"><a name="zh-cn_topic_0167929270_p446655811403"></a><a name="zh-cn_topic_0167929270_p446655811403"></a>"ecs:*:get*",</p>
<p id="zh-cn_topic_0167929270_p174662585409"><a name="zh-cn_topic_0167929270_p174662585409"></a><a name="zh-cn_topic_0167929270_p174662585409"></a>"ecs:*:list*",</p>
<p id="a9ee725cb4e6d4f60974daf0d7cf80b1c"><a name="a9ee725cb4e6d4f60974daf0d7cf80b1c"></a><a name="a9ee725cb4e6d4f60974daf0d7cf80b1c"></a>"ecs:*:create*",</p>
<p id="ac11c06d2d858415cb510e1f8bddb41f1"><a name="ac11c06d2d858415cb510e1f8bddb41f1"></a><a name="ac11c06d2d858415cb510e1f8bddb41f1"></a>"vpc:*:get*",</p>
<p id="zh-cn_topic_0167929270_p846605874012"><a name="zh-cn_topic_0167929270_p846605874012"></a><a name="zh-cn_topic_0167929270_p846605874012"></a>"vpc:*:list*",</p>
<p id="zh-cn_topic_0167929270_p175636481462"><a name="zh-cn_topic_0167929270_p175636481462"></a><a name="zh-cn_topic_0167929270_p175636481462"></a>"vpc:*:create*",</p>
<p id="a45ba0a75f23d45b49fdc1e3151efd170"><a name="a45ba0a75f23d45b49fdc1e3151efd170"></a><a name="a45ba0a75f23d45b49fdc1e3151efd170"></a>"evs:*:get*",</p>
<p id="zh-cn_topic_0167929270_p746625854020"><a name="zh-cn_topic_0167929270_p746625854020"></a><a name="zh-cn_topic_0167929270_p746625854020"></a>"evs:*:list*",</p>
<p id="aac39e70e593040589d82dae77bea7e67"><a name="aac39e70e593040589d82dae77bea7e67"></a><a name="aac39e70e593040589d82dae77bea7e67"></a>"evs:*:create*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="u203bc75846514b34972e45cb3d4f6911"></a><a name="u203bc75846514b34972e45cb3d4f6911"></a><ul id="u203bc75846514b34972e45cb3d4f6911"><li>支持：<a name="u12f0e1d27f8c4ddeb960e2e5f8029478"></a><a name="u12f0e1d27f8c4ddeb960e2e5f8029478"></a><ul id="u12f0e1d27f8c4ddeb960e2e5f8029478"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="rae12736ed2e142009d03913ffa60cac4"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="a5893ad5db9274f81a11e5306fe879ecd"><a name="a5893ad5db9274f81a11e5306fe879ecd"></a><a name="a5893ad5db9274f81a11e5306fe879ecd"></a>获取集群列表</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="a87e37268e04b4c2ebd8c5c881a6cbfb5"><a name="a87e37268e04b4c2ebd8c5c881a6cbfb5"></a><a name="a87e37268e04b4c2ebd8c5c881a6cbfb5"></a>"dws:cluster:list"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="ad16cab71fa6f4f1299bac92c8aa8c422"><a name="ad16cab71fa6f4f1299bac92c8aa8c422"></a><a name="ad16cab71fa6f4f1299bac92c8aa8c422"></a>"dws:*:get*",</p>
<p id="ae4cc23e47f21438498bbfc4f9d80e072"><a name="ae4cc23e47f21438498bbfc4f9d80e072"></a><a name="ae4cc23e47f21438498bbfc4f9d80e072"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="ud6a1539bb2664762a7eb70c18d25b05a"></a><a name="ud6a1539bb2664762a7eb70c18d25b05a"></a><ul id="ud6a1539bb2664762a7eb70c18d25b05a"><li>支持：<a name="u87e45aa1f67b48cfb7eba9d422e116c1"></a><a name="u87e45aa1f67b48cfb7eba9d422e116c1"></a><ul id="u87e45aa1f67b48cfb7eba9d422e116c1"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="rd0a7487e47404380ab8349237fc8718e"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="abc6fc059a0494c09ad1574c615d1081e"><a name="abc6fc059a0494c09ad1574c615d1081e"></a><a name="abc6fc059a0494c09ad1574c615d1081e"></a>获取单个集群详情</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="aaca02536280c45c988fb541ad1e79d7e"><a name="aaca02536280c45c988fb541ad1e79d7e"></a><a name="aaca02536280c45c988fb541ad1e79d7e"></a>"dws:cluster:getDetail"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0167929270_p39402517421"><a name="zh-cn_topic_0167929270_p39402517421"></a><a name="zh-cn_topic_0167929270_p39402517421"></a>"dws:*:get*",</p>
<p id="zh-cn_topic_0167929270_p794010510424"><a name="zh-cn_topic_0167929270_p794010510424"></a><a name="zh-cn_topic_0167929270_p794010510424"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="u902dc003b4704dff803d449908ebd69d"></a><a name="u902dc003b4704dff803d449908ebd69d"></a><ul id="u902dc003b4704dff803d449908ebd69d"><li>支持：<a name="u4d62b15614ac45e6af12d894094040af"></a><a name="u4d62b15614ac45e6af12d894094040af"></a><ul id="u4d62b15614ac45e6af12d894094040af"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="r3fcd2b8b46174788ac29587d3dc76aad"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="a97c86a66da534af8a3b30f576798f020"><a name="a97c86a66da534af8a3b30f576798f020"></a><a name="a97c86a66da534af8a3b30f576798f020"></a>设置自动快照</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0167929270_p951715398468"><a name="zh-cn_topic_0167929270_p951715398468"></a><a name="zh-cn_topic_0167929270_p951715398468"></a>"dws:cluster:setAutomatedSnapshot"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="a590a9b2c15cf456c8075aa38712f4daf"><a name="a590a9b2c15cf456c8075aa38712f4daf"></a><a name="a590a9b2c15cf456c8075aa38712f4daf"></a>"dws:*:get*",</p>
<p id="ab4eecebdbe554cc69ec23db2ed5c1ec0"><a name="ab4eecebdbe554cc69ec23db2ed5c1ec0"></a><a name="ab4eecebdbe554cc69ec23db2ed5c1ec0"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="u2d6f6ec1e7f6412cb7d13b89a781ba0e"></a><a name="u2d6f6ec1e7f6412cb7d13b89a781ba0e"></a><ul id="u2d6f6ec1e7f6412cb7d13b89a781ba0e"><li>支持：<a name="ud090c097aaf34c5a9c41f7b475a2d14e"></a><a name="ud090c097aaf34c5a9c41f7b475a2d14e"></a><ul id="ud090c097aaf34c5a9c41f7b475a2d14e"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="rbe85df4336ed472f82c4bfb03a19e45a"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0167929270_p651703920469"><a name="zh-cn_topic_0167929270_p651703920469"></a><a name="zh-cn_topic_0167929270_p651703920469"></a>设置安全参数/参数组</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0167929270_p451733910466"><a name="zh-cn_topic_0167929270_p451733910466"></a><a name="zh-cn_topic_0167929270_p451733910466"></a>"dws:cluster:setParameter"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="ac66c7563cddd429db867d27ec459d1fe"><a name="ac66c7563cddd429db867d27ec459d1fe"></a><a name="ac66c7563cddd429db867d27ec459d1fe"></a>"dws:*:get*",</p>
<p id="zh-cn_topic_0167929270_p51711250428"><a name="zh-cn_topic_0167929270_p51711250428"></a><a name="zh-cn_topic_0167929270_p51711250428"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="ucfcb4f05f523402190d8faf69ed26677"></a><a name="ucfcb4f05f523402190d8faf69ed26677"></a><ul id="ucfcb4f05f523402190d8faf69ed26677"><li>支持：<a name="u2d44c5cb761b469183155c044efedcce"></a><a name="u2d44c5cb761b469183155c044efedcce"></a><ul id="u2d44c5cb761b469183155c044efedcce"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="reccf3bd3903e46bcaea9104dfd065494"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="a8f5ec29f56d54a7ca6a6d022337abc0e"><a name="a8f5ec29f56d54a7ca6a6d022337abc0e"></a><a name="a8f5ec29f56d54a7ca6a6d022337abc0e"></a>重启集群</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="a0dcec2cbcfc84f69b14492657f18a197"><a name="a0dcec2cbcfc84f69b14492657f18a197"></a><a name="a0dcec2cbcfc84f69b14492657f18a197"></a>"dws:cluster:restart"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="a4b9bb7dd606c43fe9f55eb99d9a2a15b"><a name="a4b9bb7dd606c43fe9f55eb99d9a2a15b"></a><a name="a4b9bb7dd606c43fe9f55eb99d9a2a15b"></a>"dws:*:get*",</p>
<p id="zh-cn_topic_0167929270_p721815339423"><a name="zh-cn_topic_0167929270_p721815339423"></a><a name="zh-cn_topic_0167929270_p721815339423"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="u5277666f3c06410d949b5248620efb25"></a><a name="u5277666f3c06410d949b5248620efb25"></a><ul id="u5277666f3c06410d949b5248620efb25"><li>支持：<a name="zh-cn_topic_0167929270_ul62615134919"></a><a name="zh-cn_topic_0167929270_ul62615134919"></a><ul id="zh-cn_topic_0167929270_ul62615134919"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="r78269dfe5cd14f3595c9354ff2f56eaa"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0167929270_p451710393460"><a name="zh-cn_topic_0167929270_p451710393460"></a><a name="zh-cn_topic_0167929270_p451710393460"></a>扩容集群</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="aa30e52e866e344948c5103fb1829d1aa"><a name="aa30e52e866e344948c5103fb1829d1aa"></a><a name="aa30e52e866e344948c5103fb1829d1aa"></a>"dws:cluster:scaleOut"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="a7abdcbd73e734a6e938a1425649577d7"><a name="a7abdcbd73e734a6e938a1425649577d7"></a><a name="a7abdcbd73e734a6e938a1425649577d7"></a>"dws:*:get*",</p>
<p id="zh-cn_topic_0167929270_p24981571437"><a name="zh-cn_topic_0167929270_p24981571437"></a><a name="zh-cn_topic_0167929270_p24981571437"></a>"dws:*:list*",</p>
<p id="zh-cn_topic_0167929270_p1498273439"><a name="zh-cn_topic_0167929270_p1498273439"></a><a name="zh-cn_topic_0167929270_p1498273439"></a>"ecs:*:get*",</p>
<p id="zh-cn_topic_0167929270_p94988764311"><a name="zh-cn_topic_0167929270_p94988764311"></a><a name="zh-cn_topic_0167929270_p94988764311"></a>"ecs:*:list*",</p>
<p id="aac2ab8505c514b3e9ee2db232a48558a"><a name="aac2ab8505c514b3e9ee2db232a48558a"></a><a name="aac2ab8505c514b3e9ee2db232a48558a"></a>"ecs:*:create*",</p>
<p id="zh-cn_topic_0167929270_p84983716432"><a name="zh-cn_topic_0167929270_p84983716432"></a><a name="zh-cn_topic_0167929270_p84983716432"></a>"vpc:*:get*",</p>
<p id="zh-cn_topic_0167929270_p849867174316"><a name="zh-cn_topic_0167929270_p849867174316"></a><a name="zh-cn_topic_0167929270_p849867174316"></a>"vpc:*:list*",</p>
<p id="zh-cn_topic_0167929270_p889573435111"><a name="zh-cn_topic_0167929270_p889573435111"></a><a name="zh-cn_topic_0167929270_p889573435111"></a>"vpc:*:create*",</p>
<p id="aa37fdc7a2f7c44e0a5f2a195f0b57d60"><a name="aa37fdc7a2f7c44e0a5f2a195f0b57d60"></a><a name="aa37fdc7a2f7c44e0a5f2a195f0b57d60"></a>"evs:*:get*",</p>
<p id="ad38a8c36431c45bc9531a4d51dc78fed"><a name="ad38a8c36431c45bc9531a4d51dc78fed"></a><a name="ad38a8c36431c45bc9531a4d51dc78fed"></a>"evs:*:list*",</p>
<p id="a7915621d7ea84b42888740d6293ec28a"><a name="a7915621d7ea84b42888740d6293ec28a"></a><a name="a7915621d7ea84b42888740d6293ec28a"></a>"evs:*:create*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="zh-cn_topic_0167929270_ul63713520492"></a><a name="zh-cn_topic_0167929270_ul63713520492"></a><ul id="zh-cn_topic_0167929270_ul63713520492"><li>支持：<a name="u1b50f64b22ee4b4fbbbe04405883a9d6"></a><a name="u1b50f64b22ee4b4fbbbe04405883a9d6"></a><ul id="u1b50f64b22ee4b4fbbbe04405883a9d6"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="rc135bb62895145f0a3f621527706618c"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="aed313486b7904c21997d503f69176a16"><a name="aed313486b7904c21997d503f69176a16"></a><a name="aed313486b7904c21997d503f69176a16"></a>调整大小</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0167929270_p477434513919"><a name="zh-cn_topic_0167929270_p477434513919"></a><a name="zh-cn_topic_0167929270_p477434513919"></a>dws:openAPICluster:resize</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="ada876862469349a686195e498271627a"><a name="ada876862469349a686195e498271627a"></a><a name="ada876862469349a686195e498271627a"></a>"dws:*:get*",</p>
<p id="a4e6d640b27ed4e7fb5165265cd330e29"><a name="a4e6d640b27ed4e7fb5165265cd330e29"></a><a name="a4e6d640b27ed4e7fb5165265cd330e29"></a>"dws:*:list*",</p>
<p id="aaccd059d191948e49084d52adccfddac"><a name="aaccd059d191948e49084d52adccfddac"></a><a name="aaccd059d191948e49084d52adccfddac"></a>"ecs:*:get*",</p>
<p id="a0b5d35318aed4538bff7bdfc46edfef4"><a name="a0b5d35318aed4538bff7bdfc46edfef4"></a><a name="a0b5d35318aed4538bff7bdfc46edfef4"></a>"ecs:*:list*",</p>
<p id="a32014ec3f1bb4b58a7798253382900d9"><a name="a32014ec3f1bb4b58a7798253382900d9"></a><a name="a32014ec3f1bb4b58a7798253382900d9"></a>"ecs:*:create*",</p>
<p id="zh-cn_topic_0167929270_p426474994320"><a name="zh-cn_topic_0167929270_p426474994320"></a><a name="zh-cn_topic_0167929270_p426474994320"></a>"vpc:*:get*",</p>
<p id="zh-cn_topic_0167929270_p326415494436"><a name="zh-cn_topic_0167929270_p326415494436"></a><a name="zh-cn_topic_0167929270_p326415494436"></a>"vpc:*:list*",</p>
<p id="a5f8247e0c22c4135b7d7f865ba4557a7"><a name="a5f8247e0c22c4135b7d7f865ba4557a7"></a><a name="a5f8247e0c22c4135b7d7f865ba4557a7"></a>"vpc:*:create*",</p>
<p id="zh-cn_topic_0167929270_p182642491433"><a name="zh-cn_topic_0167929270_p182642491433"></a><a name="zh-cn_topic_0167929270_p182642491433"></a>"evs:*:get*",</p>
<p id="zh-cn_topic_0167929270_p102642499438"><a name="zh-cn_topic_0167929270_p102642499438"></a><a name="zh-cn_topic_0167929270_p102642499438"></a>"evs:*:list*",</p>
<p id="a9aa875ba8b1547aeab9f72cc44d1c208"><a name="a9aa875ba8b1547aeab9f72cc44d1c208"></a><a name="a9aa875ba8b1547aeab9f72cc44d1c208"></a>"evs:*:create*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="u4c86953d96824267b061f5681a02cfd8"></a><a name="u4c86953d96824267b061f5681a02cfd8"></a><ul id="u4c86953d96824267b061f5681a02cfd8"><li>支持：<a name="ua5a057528da349f6aa2fb3eb918ca483"></a><a name="ua5a057528da349f6aa2fb3eb918ca483"></a><ul id="ua5a057528da349f6aa2fb3eb918ca483"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="r695be33afd4a484095a6c38bed519649"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="aa0b30aada4794a91be8656e2f2d13efb"><a name="aa0b30aada4794a91be8656e2f2d13efb"></a><a name="aa0b30aada4794a91be8656e2f2d13efb"></a>重置密码</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="a499590f9db8d4633b4be1253a22385c6"><a name="a499590f9db8d4633b4be1253a22385c6"></a><a name="a499590f9db8d4633b4be1253a22385c6"></a>"dws:cluster:resetPassword"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="af0df9626e3b044b2805326e4cfbc45da"><a name="af0df9626e3b044b2805326e4cfbc45da"></a><a name="af0df9626e3b044b2805326e4cfbc45da"></a>"dws:*:get*",</p>
<p id="a0b6d1a06b9e1419d9189f35d2bcfeda7"><a name="a0b6d1a06b9e1419d9189f35d2bcfeda7"></a><a name="a0b6d1a06b9e1419d9189f35d2bcfeda7"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="u4ef916a50d2d4796867d93dcb571d63a"></a><a name="u4ef916a50d2d4796867d93dcb571d63a"></a><ul id="u4ef916a50d2d4796867d93dcb571d63a"><li>支持：<a name="u82efcef535214735b7404c30ca1801db"></a><a name="u82efcef535214735b7404c30ca1801db"></a><ul id="u82efcef535214735b7404c30ca1801db"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="r4ac2412332144220ada11fdffe32598e"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="ab1be00e918da4a11834b569e38d13d47"><a name="ab1be00e918da4a11834b569e38d13d47"></a><a name="ab1be00e918da4a11834b569e38d13d47"></a>应用参数模板</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="a6550e0fb2e904265ba60f284e9debec1"><a name="a6550e0fb2e904265ba60f284e9debec1"></a><a name="a6550e0fb2e904265ba60f284e9debec1"></a>"dws:cluster:changeParameterGroup"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0167929270_p36920325443"><a name="zh-cn_topic_0167929270_p36920325443"></a><a name="zh-cn_topic_0167929270_p36920325443"></a>"dws:*:get*",</p>
<p id="a658f0fe3bc9a4a5aa39507eeb8770c38"><a name="a658f0fe3bc9a4a5aa39507eeb8770c38"></a><a name="a658f0fe3bc9a4a5aa39507eeb8770c38"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="ub399b2ef15d84c72b033e8b7ac0d76c9"></a><a name="ub399b2ef15d84c72b033e8b7ac0d76c9"></a><ul id="ub399b2ef15d84c72b033e8b7ac0d76c9"><li>支持：<a name="zh-cn_topic_0167929270_ul62217592496"></a><a name="zh-cn_topic_0167929270_ul62217592496"></a><ul id="zh-cn_topic_0167929270_ul62217592496"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="r51a61fbfc338481891f27419174326bf"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="a4056d9432a7247a2b6f3ae362f103bea"><a name="a4056d9432a7247a2b6f3ae362f103bea"></a><a name="a4056d9432a7247a2b6f3ae362f103bea"></a>删除集群</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="acdc1e1bb3b4d4071a6e499a0a3c411c9"><a name="acdc1e1bb3b4d4071a6e499a0a3c411c9"></a><a name="acdc1e1bb3b4d4071a6e499a0a3c411c9"></a>dws:cluster:delete"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="a9e619ba767a44fac9b37ca766f9f9ff6"><a name="a9e619ba767a44fac9b37ca766f9f9ff6"></a><a name="a9e619ba767a44fac9b37ca766f9f9ff6"></a>"dws:*:get*",</p>
<p id="zh-cn_topic_0167929270_p186945495478"><a name="zh-cn_topic_0167929270_p186945495478"></a><a name="zh-cn_topic_0167929270_p186945495478"></a>"dws:*:list*",</p>
<p id="zh-cn_topic_0167929270_p369415495472"><a name="zh-cn_topic_0167929270_p369415495472"></a><a name="zh-cn_topic_0167929270_p369415495472"></a>"ecs:*:get*",</p>
<p id="a23b3db04d98b431399652252901bd1b2"><a name="a23b3db04d98b431399652252901bd1b2"></a><a name="a23b3db04d98b431399652252901bd1b2"></a>"ecs:*:list*",</p>
<p id="ab01f0e8da29140cf833d9d7a28567ad3"><a name="ab01f0e8da29140cf833d9d7a28567ad3"></a><a name="ab01f0e8da29140cf833d9d7a28567ad3"></a>"ecs:*:delete*",</p>
<p id="a99eeac5889f642e19e5195e641a25932"><a name="a99eeac5889f642e19e5195e641a25932"></a><a name="a99eeac5889f642e19e5195e641a25932"></a>"vpc:*:get*",</p>
<p id="a182c462f768c484d90d91d617f5e0ce7"><a name="a182c462f768c484d90d91d617f5e0ce7"></a><a name="a182c462f768c484d90d91d617f5e0ce7"></a>"vpc:*:list*",</p>
<p id="a0ccee16565654372aa7296ecd3633164"><a name="a0ccee16565654372aa7296ecd3633164"></a><a name="a0ccee16565654372aa7296ecd3633164"></a>"vpc:*:delete*",</p>
<p id="a16c8f0c10e874a209f0420bdf84f13bb"><a name="a16c8f0c10e874a209f0420bdf84f13bb"></a><a name="a16c8f0c10e874a209f0420bdf84f13bb"></a>"evs:*:get*",</p>
<p id="ab435d60503ac434dad545f2d8b373f62"><a name="ab435d60503ac434dad545f2d8b373f62"></a><a name="ab435d60503ac434dad545f2d8b373f62"></a>"evs:*:list*",</p>
<p id="zh-cn_topic_0167929270_p522917717592"><a name="zh-cn_topic_0167929270_p522917717592"></a><a name="zh-cn_topic_0167929270_p522917717592"></a>"evs:*:delete*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="uaf12cc113b814b578f4c3b3b5a51b4e7"></a><a name="uaf12cc113b814b578f4c3b3b5a51b4e7"></a><ul id="uaf12cc113b814b578f4c3b3b5a51b4e7"><li>支持：<a name="u20ec1e0cb90040be937e32fce0092a01"></a><a name="u20ec1e0cb90040be937e32fce0092a01"></a><ul id="u20ec1e0cb90040be937e32fce0092a01"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="ra28c7d04e7ac4016a2279cae23856cfe"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="ac96d97b1f19b43a4a17392851b7d9617"><a name="ac96d97b1f19b43a4a17392851b7d9617"></a><a name="ac96d97b1f19b43a4a17392851b7d9617"></a>设置可维护时间段</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="a03507d108eaf4317835a65254cb558c2"><a name="a03507d108eaf4317835a65254cb558c2"></a><a name="a03507d108eaf4317835a65254cb558c2"></a>"dws:cluster:setMaintainceWindow"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0167929270_p1272392440"><a name="zh-cn_topic_0167929270_p1272392440"></a><a name="zh-cn_topic_0167929270_p1272392440"></a>"dws:*:get*",</p>
<p id="a07b56bf3146c4c708bbd6c00cc2d1c35"><a name="a07b56bf3146c4c708bbd6c00cc2d1c35"></a><a name="a07b56bf3146c4c708bbd6c00cc2d1c35"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="u4577c059f55d4050a873d091b57b8124"></a><a name="u4577c059f55d4050a873d091b57b8124"></a><ul id="u4577c059f55d4050a873d091b57b8124"><li>支持：<a name="udde73d82823147259478d97afc608b47"></a><a name="udde73d82823147259478d97afc608b47"></a><ul id="udde73d82823147259478d97afc608b47"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="rb18deb3d5b944cc5bd66d674d629fe22"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="a78f7a8e989b046eaa439561d58b43f1b"><a name="a78f7a8e989b046eaa439561d58b43f1b"></a><a name="a78f7a8e989b046eaa439561d58b43f1b"></a>绑定EIP</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0167929270_p15179392462"><a name="zh-cn_topic_0167929270_p15179392462"></a><a name="zh-cn_topic_0167929270_p15179392462"></a>"dws:eip:operate"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="a6c8cfac307fb473e902eb72a41bcb09b"><a name="a6c8cfac307fb473e902eb72a41bcb09b"></a><a name="a6c8cfac307fb473e902eb72a41bcb09b"></a>"dws:*:get*",</p>
<p id="a47f3210b053e4f9aa0a59e356990ca11"><a name="a47f3210b053e4f9aa0a59e356990ca11"></a><a name="a47f3210b053e4f9aa0a59e356990ca11"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="u71107d8028bf435ca4eb1961b95c3b80"></a><a name="u71107d8028bf435ca4eb1961b95c3b80"></a><ul id="u71107d8028bf435ca4eb1961b95c3b80"><li>支持：<a name="ue23e1b838ea44da78234b896efe52821"></a><a name="ue23e1b838ea44da78234b896efe52821"></a><ul id="ue23e1b838ea44da78234b896efe52821"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="r697d14dd2b3f402eafe5b892fdb08ef8"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="a2368901f36df4cabac680ac6487236c1"><a name="a2368901f36df4cabac680ac6487236c1"></a><a name="a2368901f36df4cabac680ac6487236c1"></a>解绑EIP</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="a14d4af7f41064c7689873b4814f1da92"><a name="a14d4af7f41064c7689873b4814f1da92"></a><a name="a14d4af7f41064c7689873b4814f1da92"></a>"dws:eip:operate"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="a09f927cd4e694ab088e50e23dfb8c8ed"><a name="a09f927cd4e694ab088e50e23dfb8c8ed"></a><a name="a09f927cd4e694ab088e50e23dfb8c8ed"></a>"dws:*:get*",</p>
<p id="zh-cn_topic_0167929270_p446864674412"><a name="zh-cn_topic_0167929270_p446864674412"></a><a name="zh-cn_topic_0167929270_p446864674412"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="u41273dbc8ee543b8a61738ad46f43847"></a><a name="u41273dbc8ee543b8a61738ad46f43847"></a><ul id="u41273dbc8ee543b8a61738ad46f43847"><li>支持：<a name="ud6cab8b3290249deb53a4d0bdf8c74d7"></a><a name="ud6cab8b3290249deb53a4d0bdf8c74d7"></a><ul id="ud6cab8b3290249deb53a4d0bdf8c74d7"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="r3fcd1b136a00499892d9b980e76f3a45"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="a9d4a370e274845b89f8b6be3a47a2072"><a name="a9d4a370e274845b89f8b6be3a47a2072"></a><a name="a9d4a370e274845b89f8b6be3a47a2072"></a>创建DNS域名</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="a3b1b83036c954e968d951d0c1e15e78b"><a name="a3b1b83036c954e968d951d0c1e15e78b"></a><a name="a3b1b83036c954e968d951d0c1e15e78b"></a>"dws:dns:create"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="a4e5abc7d3f604eaaae64b09142af6935"><a name="a4e5abc7d3f604eaaae64b09142af6935"></a><a name="a4e5abc7d3f604eaaae64b09142af6935"></a>"dws:*:get*",</p>
<p id="a626f3cfc2561476d95612f150e7ffe09"><a name="a626f3cfc2561476d95612f150e7ffe09"></a><a name="a626f3cfc2561476d95612f150e7ffe09"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="ucc5a36743e5d428aacb4e94659fbb59f"></a><a name="ucc5a36743e5d428aacb4e94659fbb59f"></a><ul id="ucc5a36743e5d428aacb4e94659fbb59f"><li>支持：<a name="u69feca1d69f54e1ead0c64dbf64c0a31"></a><a name="u69feca1d69f54e1ead0c64dbf64c0a31"></a><ul id="u69feca1d69f54e1ead0c64dbf64c0a31"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="rfcb339cb7381447486fff40bced74a42"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="a328f9c31cb394265a04d0b27a277c4fb"><a name="a328f9c31cb394265a04d0b27a277c4fb"></a><a name="a328f9c31cb394265a04d0b27a277c4fb"></a>释放DNS域名</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="a5b4ef66e818d4c0d80fc10a6d3e01517"><a name="a5b4ef66e818d4c0d80fc10a6d3e01517"></a><a name="a5b4ef66e818d4c0d80fc10a6d3e01517"></a>"dws:dns:release"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0167929270_p583855364415"><a name="zh-cn_topic_0167929270_p583855364415"></a><a name="zh-cn_topic_0167929270_p583855364415"></a>"dws:*:get*",</p>
<p id="a47bad5f54bf0423199144c11e16bc6fc"><a name="a47bad5f54bf0423199144c11e16bc6fc"></a><a name="a47bad5f54bf0423199144c11e16bc6fc"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="u4bf8d7bd8fac4cdf8a506d1df196ccc4"></a><a name="u4bf8d7bd8fac4cdf8a506d1df196ccc4"></a><ul id="u4bf8d7bd8fac4cdf8a506d1df196ccc4"><li>支持：<a name="ub0b40166d47b48199aa31c02d65fc194"></a><a name="ub0b40166d47b48199aa31c02d65fc194"></a><ul id="ub0b40166d47b48199aa31c02d65fc194"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="reb75cc2600c74ee2960bca675bdd7fe3"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="acf76b6066a0b4b9b8d72b5fd17356435"><a name="acf76b6066a0b4b9b8d72b5fd17356435"></a><a name="acf76b6066a0b4b9b8d72b5fd17356435"></a>修改DNS域名</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="a8a70cdf78a434519a0e020385f5effa8"><a name="a8a70cdf78a434519a0e020385f5effa8"></a><a name="a8a70cdf78a434519a0e020385f5effa8"></a>"dws:dns:edit"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0167929270_p915917575448"><a name="zh-cn_topic_0167929270_p915917575448"></a><a name="zh-cn_topic_0167929270_p915917575448"></a>"dws:*:get*",</p>
<p id="zh-cn_topic_0167929270_p21594579449"><a name="zh-cn_topic_0167929270_p21594579449"></a><a name="zh-cn_topic_0167929270_p21594579449"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="u1c9b0a98eb794f20899c0b5fa74a3be9"></a><a name="u1c9b0a98eb794f20899c0b5fa74a3be9"></a><ul id="u1c9b0a98eb794f20899c0b5fa74a3be9"><li>支持：<a name="zh-cn_topic_0167929270_ul91718156508"></a><a name="zh-cn_topic_0167929270_ul91718156508"></a><ul id="zh-cn_topic_0167929270_ul91718156508"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="r3a644f9926474754b19c620483144c7f"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="aa830c41ff09b4e1185035616d6347aa3"><a name="aa830c41ff09b4e1185035616d6347aa3"></a><a name="aa830c41ff09b4e1185035616d6347aa3"></a>创建MRS连接</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="a2891ba2e663345ccb6e2c726d4e8bdf7"><a name="a2891ba2e663345ccb6e2c726d4e8bdf7"></a><a name="a2891ba2e663345ccb6e2c726d4e8bdf7"></a>"dws:MRSConnection:create"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0167929270_p63537134515"><a name="zh-cn_topic_0167929270_p63537134515"></a><a name="zh-cn_topic_0167929270_p63537134515"></a>"dws:*:get*",</p>
<p id="zh-cn_topic_0167929270_p0353315459"><a name="zh-cn_topic_0167929270_p0353315459"></a><a name="zh-cn_topic_0167929270_p0353315459"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="u142ce6618ee247d79a50544988181f7d"></a><a name="u142ce6618ee247d79a50544988181f7d"></a><ul id="u142ce6618ee247d79a50544988181f7d"><li>支持：<a name="u3695fcb6f988499391efdef8d6533b48"></a><a name="u3695fcb6f988499391efdef8d6533b48"></a><ul id="u3695fcb6f988499391efdef8d6533b48"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="r2fd5b9d0ae7e4e07a0191f0f34e34190"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="a129d8aa3d9db407893d3f10f8204078d"><a name="a129d8aa3d9db407893d3f10f8204078d"></a><a name="a129d8aa3d9db407893d3f10f8204078d"></a>更新MRS连接</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="ae674f9ebc3f0485295158eb4c458e7ac"><a name="ae674f9ebc3f0485295158eb4c458e7ac"></a><a name="ae674f9ebc3f0485295158eb4c458e7ac"></a>"dws:MRSConnection:update"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0167929270_p12506849455"><a name="zh-cn_topic_0167929270_p12506849455"></a><a name="zh-cn_topic_0167929270_p12506849455"></a>"dws:*:get*",</p>
<p id="abb89cb1accdc4136950bf751bb6ae296"><a name="abb89cb1accdc4136950bf751bb6ae296"></a><a name="abb89cb1accdc4136950bf751bb6ae296"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="u730e765de7a64959a6417fc2af77d62a"></a><a name="u730e765de7a64959a6417fc2af77d62a"></a><ul id="u730e765de7a64959a6417fc2af77d62a"><li>支持：<a name="u81eac5ed104641df84d89644caa3a1e9"></a><a name="u81eac5ed104641df84d89644caa3a1e9"></a><ul id="u81eac5ed104641df84d89644caa3a1e9"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="r50138630bd4548878292199bbb8b0eeb"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="a15aa738a1a714de48b3a400d49e25711"><a name="a15aa738a1a714de48b3a400d49e25711"></a><a name="a15aa738a1a714de48b3a400d49e25711"></a>删除MRS连接</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="a0bd4ed896cb44abeab13b1836fcfb164"><a name="a0bd4ed896cb44abeab13b1836fcfb164"></a><a name="a0bd4ed896cb44abeab13b1836fcfb164"></a>"dws:MRSConnection:delete"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0167929270_p83521582455"><a name="zh-cn_topic_0167929270_p83521582455"></a><a name="zh-cn_topic_0167929270_p83521582455"></a>"dws:*:get*",</p>
<p id="zh-cn_topic_0167929270_p13531683451"><a name="zh-cn_topic_0167929270_p13531683451"></a><a name="zh-cn_topic_0167929270_p13531683451"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="udf0660ddfd3240a7aea4918333e43d89"></a><a name="udf0660ddfd3240a7aea4918333e43d89"></a><ul id="udf0660ddfd3240a7aea4918333e43d89"><li>支持：<a name="ubecac1feabad43ed8c69c3524378d70d"></a><a name="ubecac1feabad43ed8c69c3524378d70d"></a><ul id="ubecac1feabad43ed8c69c3524378d70d"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="r32f0f6ac2a274a13927f3fae129d4178"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="a3d679ac6e88b4ba8b2d49d23022eac5c"><a name="a3d679ac6e88b4ba8b2d49d23022eac5c"></a><a name="a3d679ac6e88b4ba8b2d49d23022eac5c"></a>添加/删除标签</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="ad287aab6b04b48deac338c971dda54c7"><a name="ad287aab6b04b48deac338c971dda54c7"></a><a name="ad287aab6b04b48deac338c971dda54c7"></a>"dws:tag:addAndDelete"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0167929270_p352351194520"><a name="zh-cn_topic_0167929270_p352351194520"></a><a name="zh-cn_topic_0167929270_p352351194520"></a>"dws:*:get*",</p>
<p id="zh-cn_topic_0167929270_p652313117456"><a name="zh-cn_topic_0167929270_p652313117456"></a><a name="zh-cn_topic_0167929270_p652313117456"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="uc159ea9e8392432487efc773aa70085d"></a><a name="uc159ea9e8392432487efc773aa70085d"></a><ul id="uc159ea9e8392432487efc773aa70085d"><li>支持：<a name="uaff9c79994dc4b4795d1cf67800788c1"></a><a name="uaff9c79994dc4b4795d1cf67800788c1"></a><ul id="uaff9c79994dc4b4795d1cf67800788c1"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="r24683cbdca294c7e9092455bed0c70a8"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0167929270_p951953984616"><a name="zh-cn_topic_0167929270_p951953984616"></a><a name="zh-cn_topic_0167929270_p951953984616"></a>编辑标签</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0167929270_p125197391461"><a name="zh-cn_topic_0167929270_p125197391461"></a><a name="zh-cn_topic_0167929270_p125197391461"></a>"dws:tag:edit"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="a9102a73f9e7b46d7810b2c594f7b6c82"><a name="a9102a73f9e7b46d7810b2c594f7b6c82"></a><a name="a9102a73f9e7b46d7810b2c594f7b6c82"></a>"dws:*:get*",</p>
<p id="zh-cn_topic_0167929270_p153886151456"><a name="zh-cn_topic_0167929270_p153886151456"></a><a name="zh-cn_topic_0167929270_p153886151456"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="u179d721f05ba4c1a80c49175ff7432af"></a><a name="u179d721f05ba4c1a80c49175ff7432af"></a><ul id="u179d721f05ba4c1a80c49175ff7432af"><li>支持：<a name="ub0b38f08f37e455f9ae304e3414df5bf"></a><a name="ub0b38f08f37e455f9ae304e3414df5bf"></a><ul id="ub0b38f08f37e455f9ae304e3414df5bf"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="r1903111e161242168ea07cb336377f1b"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0167929270_p551923934612"><a name="zh-cn_topic_0167929270_p551923934612"></a><a name="zh-cn_topic_0167929270_p551923934612"></a>创建快照</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="af4ac31b90ff548aa822d491356028b2f"><a name="af4ac31b90ff548aa822d491356028b2f"></a><a name="af4ac31b90ff548aa822d491356028b2f"></a>"dws:snapshot:create"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0167929270_p82031917457"><a name="zh-cn_topic_0167929270_p82031917457"></a><a name="zh-cn_topic_0167929270_p82031917457"></a>"dws:*:get*",</p>
<p id="ae4e71b5573eb49879ed3c08aa62df512"><a name="ae4e71b5573eb49879ed3c08aa62df512"></a><a name="ae4e71b5573eb49879ed3c08aa62df512"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="u61e1c96d415b495697e61b417bbf7871"></a><a name="u61e1c96d415b495697e61b417bbf7871"></a><ul id="u61e1c96d415b495697e61b417bbf7871"><li>支持：<a name="zh-cn_topic_0167929270_ul47069535503"></a><a name="zh-cn_topic_0167929270_ul47069535503"></a><ul id="zh-cn_topic_0167929270_ul47069535503"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="r2801ba8279a84ff5adb390ee10d0b040"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0167929270_p698519113443"><a name="zh-cn_topic_0167929270_p698519113443"></a><a name="zh-cn_topic_0167929270_p698519113443"></a>获取快照列表</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0167929270_p8756712407"><a name="zh-cn_topic_0167929270_p8756712407"></a><a name="zh-cn_topic_0167929270_p8756712407"></a>"dws:snapshot:list"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="a7ff544f1708541559de303d3b94f190d"><a name="a7ff544f1708541559de303d3b94f190d"></a><a name="a7ff544f1708541559de303d3b94f190d"></a>"dws:*:get*"</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="udb80cf5e8c934f3c8d21b4343d2c8e20"></a><a name="udb80cf5e8c934f3c8d21b4343d2c8e20"></a><ul id="udb80cf5e8c934f3c8d21b4343d2c8e20"><li>支持：<a name="u3ff7c77978a648478d7b582fe9a2c984"></a><a name="u3ff7c77978a648478d7b582fe9a2c984"></a><ul id="u3ff7c77978a648478d7b582fe9a2c984"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="rcc22a4a0b4954c9ea191d71038c03ea8"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0167929270_p751973915466"><a name="zh-cn_topic_0167929270_p751973915466"></a><a name="zh-cn_topic_0167929270_p751973915466"></a>删除快照</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="afecaf94b0b7d487884b7dea6fd31cf1c"><a name="afecaf94b0b7d487884b7dea6fd31cf1c"></a><a name="afecaf94b0b7d487884b7dea6fd31cf1c"></a>"dws:snapshot:delete"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0167929270_p242145114716"><a name="zh-cn_topic_0167929270_p242145114716"></a><a name="zh-cn_topic_0167929270_p242145114716"></a>"dws:snapshot:list"</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="uf0ec1ca992124a4bbaafae8ec2b38da5"></a><a name="uf0ec1ca992124a4bbaafae8ec2b38da5"></a><ul id="uf0ec1ca992124a4bbaafae8ec2b38da5"><li>支持：<a name="u574ae424cd5048fd9d03d41f197b4bb1"></a><a name="u574ae424cd5048fd9d03d41f197b4bb1"></a><ul id="u574ae424cd5048fd9d03d41f197b4bb1"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="rd336c6af377a4abdadb2bacf412d69ac"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="afd8a5484624a43db8db973881235518b"><a name="afd8a5484624a43db8db973881235518b"></a><a name="afd8a5484624a43db8db973881235518b"></a>复制快照</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="ab6b793a8e6fd4fd5a9e788e7abaa7684"><a name="ab6b793a8e6fd4fd5a9e788e7abaa7684"></a><a name="ab6b793a8e6fd4fd5a9e788e7abaa7684"></a>"dws:snapshot:copy"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0167929270_p131752194713"><a name="zh-cn_topic_0167929270_p131752194713"></a><a name="zh-cn_topic_0167929270_p131752194713"></a>"dws:snapshot:list"</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="u002db40850254c02bd8e2f46386c7fb7"></a><a name="u002db40850254c02bd8e2f46386c7fb7"></a><ul id="u002db40850254c02bd8e2f46386c7fb7"><li>支持：<a name="ube25f4ad7e674c10ae2ed46c354dc3ae"></a><a name="ube25f4ad7e674c10ae2ed46c354dc3ae"></a><ul id="ube25f4ad7e674c10ae2ed46c354dc3ae"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="rea549d967c5649a2aed93cfa5ed225a2"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0167929270_p151911399466"><a name="zh-cn_topic_0167929270_p151911399466"></a><a name="zh-cn_topic_0167929270_p151911399466"></a>创建参数模板</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0167929270_p125199398465"><a name="zh-cn_topic_0167929270_p125199398465"></a><a name="zh-cn_topic_0167929270_p125199398465"></a>"dws:parameterGroup:create"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="a18f7eb72f0bd41fcab7e22810d5a3053"><a name="a18f7eb72f0bd41fcab7e22810d5a3053"></a><a name="a18f7eb72f0bd41fcab7e22810d5a3053"></a>"dws:*:get*",</p>
<p id="aa09c27491c2647c48fbbf76303f583af"><a name="aa09c27491c2647c48fbbf76303f583af"></a><a name="aa09c27491c2647c48fbbf76303f583af"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="zh-cn_topic_0167929270_ul18618313517"></a><a name="zh-cn_topic_0167929270_ul18618313517"></a><ul id="zh-cn_topic_0167929270_ul18618313517"><li>支持：<a name="u867e6926704946d2a4f058731e7a75bf"></a><a name="u867e6926704946d2a4f058731e7a75bf"></a><ul id="u867e6926704946d2a4f058731e7a75bf"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="r1e2ecf002ade4169a2be4e608f2c89d4"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="aa3e0c79d55524f47ba53e0316ceffa1d"><a name="aa3e0c79d55524f47ba53e0316ceffa1d"></a><a name="aa3e0c79d55524f47ba53e0316ceffa1d"></a>删除参数模板</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="abd799d92cac5452dbcfd33426b9e1c56"><a name="abd799d92cac5452dbcfd33426b9e1c56"></a><a name="abd799d92cac5452dbcfd33426b9e1c56"></a>"dws:parameterGroup:delete"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="ac06d496e3aab45a6bbb434aa31fef55f"><a name="ac06d496e3aab45a6bbb434aa31fef55f"></a><a name="ac06d496e3aab45a6bbb434aa31fef55f"></a>"dws:*:get*",</p>
<p id="ab18a6d61c47b4771a80aa2060b863f88"><a name="ab18a6d61c47b4771a80aa2060b863f88"></a><a name="ab18a6d61c47b4771a80aa2060b863f88"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="zh-cn_topic_0167929270_ul19641148513"></a><a name="zh-cn_topic_0167929270_ul19641148513"></a><ul id="zh-cn_topic_0167929270_ul19641148513"><li>支持：<a name="u33a273176d6e4610bd96a63b4b7acbd5"></a><a name="u33a273176d6e4610bd96a63b4b7acbd5"></a><ul id="u33a273176d6e4610bd96a63b4b7acbd5"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="r863e289e5f854d6cbc9671912398e294"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="a38fcd9c35f1a4f02acf4b489c9132ade"><a name="a38fcd9c35f1a4f02acf4b489c9132ade"></a><a name="a38fcd9c35f1a4f02acf4b489c9132ade"></a>修改参数模板</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="a106a117a354846c8bcf2e39074808598"><a name="a106a117a354846c8bcf2e39074808598"></a><a name="a106a117a354846c8bcf2e39074808598"></a>"dws:parameterGroup:edit"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="a9c53856013904332940d252ebb7da90c"><a name="a9c53856013904332940d252ebb7da90c"></a><a name="a9c53856013904332940d252ebb7da90c"></a>"dws:*:get*",</p>
<p id="a28d1a048e39d491bb60fc700abb5e4b9"><a name="a28d1a048e39d491bb60fc700abb5e4b9"></a><a name="a28d1a048e39d491bb60fc700abb5e4b9"></a>"dws:*:list*",</p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="u0294f0043df84cc28884c2a69a19c05f"></a><a name="u0294f0043df84cc28884c2a69a19c05f"></a><ul id="u0294f0043df84cc28884c2a69a19c05f"><li>支持：<a name="ue7e85f9a60be4069ac759dbba6e89f78"></a><a name="ue7e85f9a60be4069ac759dbba6e89f78"></a><ul id="ue7e85f9a60be4069ac759dbba6e89f78"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="row75751622141419"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="p202831218191513"><a name="p202831218191513"></a><a name="p202831218191513"></a>终止查询</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="p19576722181412"><a name="p19576722181412"></a><a name="p19576722181412"></a>"dws:query:terminate"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="p39751232134211"><a name="p39751232134211"></a><a name="p39751232134211"></a>"dws:openAPICluster:list"</p>
<p id="p10975932164219"><a name="p10975932164219"></a><a name="p10975932164219"></a></p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="ul183314220142"></a><a name="ul183314220142"></a><ul id="ul183314220142"><li>支持：<a name="ul1183414425143"></a><a name="ul1183414425143"></a><ul id="ul1183414425143"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="row11664326181417"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="p192896464193"><a name="p192896464193"></a><a name="p192896464193"></a>终止会话</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="p1830793914198"><a name="p1830793914198"></a><a name="p1830793914198"></a>"dws:session:terminate"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="p18849123711520"><a name="p18849123711520"></a><a name="p18849123711520"></a></p>
<p id="p15421935124216"><a name="p15421935124216"></a><a name="p15421935124216"></a>"dws:openAPICluster:list"</p>
<p id="p55421135154213"><a name="p55421135154213"></a><a name="p55421135154213"></a></p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="ul18976146181414"></a><a name="ul18976146181414"></a><ul id="ul18976146181414"><li>支持：<a name="ul1797613469148"></a><a name="ul1797613469148"></a><ul id="ul1797613469148"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="row052113014147"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="p20140264201"><a name="p20140264201"></a><a name="p20140264201"></a>启停DMS监控服务</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="p185135971910"><a name="p185135971910"></a><a name="p185135971910"></a>"dws:dmsService:enableOrDisable"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="p20894338151511"><a name="p20894338151511"></a><a name="p20894338151511"></a></p>
<p id="p12275938184218"><a name="p12275938184218"></a><a name="p12275938184218"></a>"dws:openAPICluster:list"</p>
<p id="p1827533813425"><a name="p1827533813425"></a><a name="p1827533813425"></a></p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="ul11705164841410"></a><a name="ul11705164841410"></a><ul id="ul11705164841410"><li>支持：<a name="ul10705948201420"></a><a name="ul10705948201420"></a><ul id="ul10705948201420"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="row1475233418147"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="p128742515205"><a name="p128742515205"></a><a name="p128742515205"></a>启停DMS监控采集项</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="p885251417206"><a name="p885251417206"></a><a name="p885251417206"></a>"dws:dmsCollectItem:enableOrDisable"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="p6708163931518"><a name="p6708163931518"></a><a name="p6708163931518"></a></p>
<p id="p95010412426"><a name="p95010412426"></a><a name="p95010412426"></a>"dws:openAPICluster:list"</p>
<p id="p3501114110422"><a name="p3501114110422"></a><a name="p3501114110422"></a></p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="ul1959113491143"></a><a name="ul1959113491143"></a><ul id="ul1959113491143"><li>支持：<a name="ul45911449201417"></a><a name="ul45911449201417"></a><ul id="ul45911449201417"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="row17546163816141"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="p1289233902014"><a name="p1289233902014"></a><a name="p1289233902014"></a>修改DMS监控采集配置</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="p3854153211209"><a name="p3854153211209"></a><a name="p3854153211209"></a>"dws:dmsCollectConfig:modify"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="p186104018156"><a name="p186104018156"></a><a name="p186104018156"></a></p>
<p id="p112853447429"><a name="p112853447429"></a><a name="p112853447429"></a>"dws:openAPICluster:list"</p>
<p id="p17285044184216"><a name="p17285044184216"></a><a name="p17285044184216"></a></p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="ul16797135015142"></a><a name="ul16797135015142"></a><ul id="ul16797135015142"><li>支持：<a name="ul7797115011148"></a><a name="ul7797115011148"></a><ul id="ul7797115011148"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
<tr id="row13414165510155"><td class="cellrowborder" valign="top" width="22.6%" headers="mcps1.2.5.1.1 "><p id="p177851444182013"><a name="p177851444182013"></a><a name="p177851444182013"></a>修改DMS存储配置</p>
</td>
<td class="cellrowborder" valign="top" width="31.81%" headers="mcps1.2.5.1.2 "><p id="p178321750182018"><a name="p178321750182018"></a><a name="p178321750182018"></a>"dws:dmsStorageConfig:modify"</p>
</td>
<td class="cellrowborder" valign="top" width="26.21%" headers="mcps1.2.5.1.3 "><p id="p835285791511"><a name="p835285791511"></a><a name="p835285791511"></a></p>
<p id="p676416469428"><a name="p676416469428"></a><a name="p676416469428"></a>"dws:openAPICluster:list"</p>
<p id="p07641646184212"><a name="p07641646184212"></a><a name="p07641646184212"></a></p>
</td>
<td class="cellrowborder" valign="top" width="19.38%" headers="mcps1.2.5.1.4 "><a name="ul18352205710155"></a><a name="ul18352205710155"></a><ul id="ul18352205710155"><li>支持：<a name="ul103527571152"></a><a name="ul103527571152"></a><ul id="ul103527571152"><li>项目(Project)</li><li>企业项目(Enterprise Project)</li></ul>
</li></ul>
</td>
</tr>
</tbody>
</table>

