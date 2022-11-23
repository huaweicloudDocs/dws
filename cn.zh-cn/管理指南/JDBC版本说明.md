# JDBC版本说明<a name="ZH-CN_TOPIC_0000001455917029"></a>

## 版本 8.2.0<a name="section336753974214"></a>

-   新增特性：兼容Oracle Raw数据类型，使用方式如下：
    -   插入或修改

        ```
        byte[] bytes = oracleResultSet.getBytes(2)
        prepareStatement.setBytes(bytes)
        //或者
        prepareStatement.setObject(bytes)
        ```

    -   查询

        ```
        resultSet.getBytes()
        resultSet.getObject()
        ```


-   修复bug

    getColumnDisplaySize\(\)方法获取字段长度错误问题。


-   修复漏洞

    CVE-2022-26520

    CVE-2022-31197


## 版本 8.1.3.100<a name="section13824125914446"></a>

-   新增特性

    支持通过resultSet.getNString获取nvarchar2对象。

-   修复漏洞

    依赖包fastjson升级到1.2.83。


## 版本 8.1.3<a name="section1769165512595"></a>

升级至开源版本42.2.23

-   新增特性

    支持nvarchar2类型

    支持通过resultSet.getObject获取nvarchar2对象


-   修复漏洞

    CVE-2022-21724


## 版本 8.1.1.300<a name="section19756125117346"></a>

-   新增特性
    -   支持nvarchar2类型。
    -   支持通过resultSet.getObject获取nvarchar2对象。


-   修复漏洞

## 版本 8.1.1.100<a name="section13434115185011"></a>

-   新增特性

    驱动默认上报操作系统用户，可指定connectionExtraInfo=false关闭。

    ```
    jdbc:postgresql://host:port/database?connectionExtraInfo=false
    ```


-   修复漏洞

    jackson升级


