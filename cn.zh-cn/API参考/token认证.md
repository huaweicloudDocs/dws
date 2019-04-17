# Token认证<a name="dws_02_0006"></a>

## 应用场景<a name="sb3ab9d18f149472589a0e172b50c909b"></a>

调用接口采用Token认证方式，通过Token认证调用请求。

当您使用Token认证方式完成认证鉴权时，需要获取用户Token并在调用接口时增加“X-Auth-Token”到业务接口请求消息头中。

本节介绍如何调用接口完成Token认证。

## 调用接口步骤<a name="s30966dd89b974431b4a2dc5585f57591"></a>

1.  发送获取用户Token的请求“POST https://_**IAM的Endpoint**_/v3/auth/tokens”。

    请求中的参数“IAM的Endpoint”，请参考[地区和终端节点](https://developer.huaweicloud.com/dev/endpoint?IAM)进行获取。

    获取请求消息体中的以下参数：

    -   user name：用户名称。
    -   user password：用户登录时的密码。
    -   domain name：用户所属的企业账户名称。
    -   project id：项目ID，请参考[获取项目编号](获取项目编号.md)进行获取。假设id是"0215ef11e49d4743be23dd97a1561e91"。

    请求内容示例如下： 

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >下面示例代码中的斜体字需要替换为实际内容，详情请参考《统一身份认证服务API参考》。  

    ```
    {
      "auth": {
        "identity": {
          "methods": [
            "password"
          ],
          "password": {
            "user": {
              "name": "username",
              "password": "password",
              "domain": {
                "name": "domainname"
              }
            }
          }
        },
        "scope": {
          "project": {
            "id": "0215ef11e49d4743be23dd97a1561e91"      
          }
        }
      }
    }
    ```

2.  <a name="l2991087a806f4324880c876ff3747400"></a>获取Token，请参考《统一身份认证服务API参考》的“获取用户Token”章节。请求响应成功后在响应消息头中包含的“X-Subject-Token”的值即为Token值。
3.  调用业务接口，在请求消息头中增加“X-Auth-Token”，“X-Auth-Token”的取值为[2](#l2991087a806f4324880c876ff3747400)中获取的Token。

