# Token认证<a name="dws_02_0006"></a>

## 应用场景<a name="sb3ab9d18f149472589a0e172b50c909b"></a>

调用接口采用Token认证方式，通过Token认证调用请求。

当您使用Token认证方式完成认证鉴权时，需要获取用户Token并在调用接口时增加“X-Auth-Token”到业务接口请求消息头中。

本节介绍如何调用接口完成Token认证。

## 调用接口步骤<a name="s30966dd89b974431b4a2dc5585f57591"></a>

1.  发送“POST https://_**IAM的Endpoint**_/v3/auth/tokens”，获取IAM的Endpoint及消息体中的区域名称。

    请参考[地区和终端节点](http://developer.huaweicloud.com/dev/endpoint)。

    当服务区域名称为“所有”时，选择IAM“华北-北京一”的Endpoint。

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
            "id": "0215ef11e49d4743be23dd97a1561e91" //假设id是"0215ef11e49d4743be23dd97a1561e91"       
          }
        }
      }
    }
    ```

2.  <a name="l2991087a806f4324880c876ff3747400"></a>获取Token，请参考《统一身份认证服务API参考》的“获取用户Token”章节。请求响应成功后在响应消息头中包含的“X-Subject-Token”的值即为Token值。
3.  调用业务接口，在请求消息头中增加“X-Auth-Token”，“X-Auth-Token”的取值为[2](#l2991087a806f4324880c876ff3747400)中获取的Token。

