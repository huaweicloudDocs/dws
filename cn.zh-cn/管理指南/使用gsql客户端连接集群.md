# 使用gsql客户端连接集群<a name="ZH-CN_TOPIC_0000001145816537"></a>

用户在创建好数据仓库集群，开始使用集群数据库之前，需要使用数据库SQL客户端连接到数据库。GaussDB\(DWS\) 提供了与集群版本配套的gsql命令行客户端工具，您可以使用gsql客户端通过集群的公网地址或者内网地址访问集群。

## 使用gsql命令行客户端连接集群<a name="section2664278815443"></a>

1.  准备一个Linux弹性云服务器，用于安装和运行gsql客户端。

    具体操作请参见[准备ECS作为gsql客户端主机](准备ECS作为gsql客户端主机.md)。

2.  请参见[下载客户端](下载客户端.md)下载gsql客户端，并使用SSH文件传输工具（例如WinSCP工具），将客户端工具上传到一个待安装gsql的Linux主机上。

    执行上传gsql操作的用户需要对客户端主机的目标存放目录有完全控制权限。

    或者，您也可以先SSH远程登录到需要安装gsql的Linux主机，然后在Linux命令窗口，执行以下命令下载gsql客户端：

    ```
    wget https://obs.myhuaweicloud.com/dws/download/dws_client_8.1.x_redhat_x64.zip --no-check-certificate
    ```

3.  使用SSH会话工具，远程登录客户端主机。

    弹性云服务器的登录方法请参见《弹性云服务器用户指南》中的[SSH密码方式登录](https://support.huaweicloud.com/usermanual-ecs/zh-cn_topic_0017955633.html)章节。

4.  （可选）如果要使用SSL方式连接集群，请参考[使用SSL进行安全的TCP/IP连接](使用SSL进行安全的TCP-IP连接.md)章节，在客户端主机配置SSL认证相关的参数。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >SSL连接方式的安全性高于非SSL方式，建议在客户端使用SSL连接方式。

5.  执行以下命令解压客户端工具。

    ```
    cd <客户端存放路径>
    unzip dws_client_redhat_x86.zip
    ```

    其中：

    -   <客户端存放路径\>：请替换为实际的客户端存放路径。
    -   dws\_client\_redhat\_x86.zip：这是“RedHat x86“对应的客户端工具包名称，请替换为实际下载的包名。

6.  执行以下命令配置客户端。

    ```
    source gsql_env.sh
    ```

    提示以下信息表示客户端已配置成功

    ```
    All things done.
    ```

7.  执行以下命令，使用gsql客户端连接GaussDB\(DWS\) 集群中的数据库。

    ```
    gsql -d <数据库名称> -h <集群地址> -U <数据库用户> -p <数据库端口> -r
    ```

    参数说明如下：

    -   “数据库名称“：输入所要连接的数据库名称。首次使用客户端连接集群时，请指定为集群的默认数据库“gaussdb“。
    -   “集群地址“：请参见[获取集群连接地址](获取集群连接地址.md)进行获取。如果通过公网地址连接，请指定为集群“公网访问地址“或“公网访问域名“，如果通过内网地址连接，请指定为集群“内网访问地址“或“内网访问域名“。
    -   “数据库用户“：输入集群数据库的用户名。首次使用客户端连接集群时，请指定为创建集群时设置的默认管理员用户，例如“dbadmin“。
    -   “数据库端口“：输入创建集群时设置的“数据库端口“。

    例如，执行以下命令连接GaussDB\(DWS\) 集群的默认数据库gaussdb：

    ```
    gsql -d gaussdb -h 10.168.0.74 -U dbadmin -p 8000 -r
    ```

    根据界面提示输入密码后，显示如下信息表示gsql工具已经连接成功：

    ```
    gaussdb=>
    ```


## gsql命令参考<a name="section41003216539"></a>

有关gsql的命令参考和更多信息，请参见[《数据仓库服务工具指南》](https://support.huaweicloud.com/tg-dws/dws_07_0001.html)。

## （可选）使用gsql导入TPC-DS样例数据<a name="section16360114045919"></a>

GaussDB\(DWS\) 支持用户将数据从集群外导入到集群中。用户可以参考以下指导，快速将样例数据从OBS导入集群，并对样例数据进行查询和分析。导入的样例数据是使用TPC-DS测试基准生成的标准性能测试数据。

TPC-DS是数据库决策支持测试基准。通过使用TPC-DS的测试数据以及测试案例，用户可以模拟真实场景下大数据集的统计、报表生成、联机查询、数据挖掘等复杂场景，从而了解数据库应用的功能和性能。

>![](public_sys-resources/icon-note.gif) **说明：** 
>当前TPC-DS样例数据仅支持在“北京一”区域导入，其他区域暂不支持。

1.  使用SSH远程连接工具登录gsql客户端主机，并进入gsql目录，本例假设gsql客户端放在/opt目录下。

    ```
    cd /opt
    ```

2.  执行以下命令，切换到指定目录并设置用户导入样例数据的用户密钥和OBS访问地址。

    ```
    cd sample
    /bin/bash setup.sh -ak <Access_Key_Id> -sk <Secret_Access_Key> -obs_location obs.cn-north-1.myhuaweicloud.com
    ```

    系统显示以下信息表示设置成功：

    ```
    setup successfully!
    ```

    >![](public_sys-resources/icon-note.gif) **说明：** 
    ><Access\_Key\_Id\>和<Secret\_Access\_Key\>：分别表示访问密钥ID和私有访问密钥。请参见[创建访问密钥（AK和SK）](https://support.huaweicloud.com/devg-dws/dws_04_0183.html)进行获取。然后，将获取到的值替换到创建外表语句中。

3.  返回上一级目录，执行gsql环境变量。

    ```
    cd ..
    source gsql_env.sh
    cd bin
    ```

4.  执行以下命令，将样例数据导入数据仓库。

    命令格式：

    ```
    gsql -d <数据库名称> -h <集群公网访问地址> -U <管理员用户> -p <数据仓库端口> -f <样例数据脚本保存路径> -r
    ```

    命令示例：

    ```
    gsql -d gaussdb -h 10.168.0.74 -U dbadmin -p 8000 -f /opt/sample/tpcds_load_data_from_obs.sql -r
    ```

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >命令中样例数据脚本“tpcds\_load\_data\_from\_obs.sql“存放在GaussDB\(DWS\) 客户端的sample目录下，如“/opt/sample/”。

    根据界面提示输入管理员密码，成功连接集群数据库后，系统会自动创建样例数据对应的外表用于关联集群外的数据，然后再创建存放样例数据的目标表，最后通过外表将数据导入到目标表中。

    由于数据集较大，导入时间取决于当前DWS集群规格，一般为10\~20分钟左右，等待系统显示如下执行时间信息表示导入成功，如下时间仅为示例。

    ```
    Time:1845600.524 ms
    ```


1.  在Linux命令窗口，执行以下命令，切换到指定目录并查询样例数据。

    ```
    cd /opt/sample/query_sql/
    /bin/bash tpcds100x.sh
    ```

2.  根据命令提示，输入集群公网访问地址的IP地址、数据库端口、数据库名称、数据库访问用户以及用户密码。

    -   数据库名称默认为“gaussdb“。
    -   数据库访问用户和密码使用创建集群时配置的管理员用户和密码。

    查询完成后，在当前查询目录，如“sample/query\_sql/“下面会生成一个存放查询结果的目录，命名如“query\_output\_20170914\_072341”。


