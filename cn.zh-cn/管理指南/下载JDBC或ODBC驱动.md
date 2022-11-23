# 下载JDBC或ODBC驱动<a name="ZH-CN_TOPIC_0000001455716749"></a>

JDBC或ODBC驱动程序用于连接GaussDB\(DWS\) 集群，用户可以在管理控制台下载GaussDB\(DWS\) 提供的JDBC或ODBC驱动程序，也可以使用开源的JDBC或ODBC驱动程序。

## 支持的开源JDBC或ODBC驱动程序<a name="section583116715476"></a>

GaussDB\(DWS\) 也支持开源的JDBC驱动程序：PostgreSQL JDBC驱动程序9.3-1103或更高版本。

GaussDB\(DWS\) 也支持开源的ODBC驱动程序：PostgreSQL ODBC 09.01.0200或更高版本。

## 下载JDBC或ODBC驱动程序<a name="section8483877102527"></a>

1.  登录GaussDB\(DWS\) 管理控制台。
2.  在左侧导航栏中，单击“连接管理“。
3.  在“下载驱动程序“区域，选择一个驱动下载。

    **图 1**  下载驱动<a name="fig16536268429"></a>  
    ![](figures/下载驱动.png "下载驱动")

    -   **JDBC驱动**

        方式一：

        选择“DWS JDBC Driver”，然后单击“下载”可以下载与现有集群版本匹配的JDBC驱动。驱动包名为“dws\_8.1.x\_jdbc\_driver.zip”，解压后有两个JDBC的驱动jar包，分别为“gsjdbc4.jar”和“gsjdbc200.jar”。

        -   gsjdbc4.jar：与PostgreSQL保持兼容，其中类名、类结构与PostgreSQL驱动完全一致，曾经运行于PostgreSQL的应用程序可以直接移植到当前系统中使用。
        -   gsjdbc200.jar：如果同一JVM进程内需要同时访问PostgreSQL及GaussDB\(DWS\) 请使用该驱动包。该包主类名为“com.huawei.gauss200.jdbc.Driver”（即将“org.postgresql”替换为“com.huawei.gauss200.jdbc”） ,数据库连接的URL前缀为“jdbc:gaussdb”，其余与gsjdbc4.jar相同。

        如果同时拥有不同版本的集群，单击“下载”时会下载与集群最低版本相对应的JDBC驱动。如果当前没有集群，单击“下载”时将下载到低版本的JDBC驱动。GaussDB\(DWS\) 集群可向下兼容低版本的JDBC驱动。

        单击“历史版本”可根据集群版本下载相应版本的JDBC驱动，建议按集群版本进行下载。

        JDBC驱动包支持在所有平台所有版本中使用，且依赖JDK 1.6及以上版本。

        如果同时拥有不同版本的集群，系统会弹出对话框，提示您选择“集群版本“然后下载与集群版本相对应的驱动程序。在“集群管理“页面的集群列表中，单击指定集群的名称，再选择“集群详情“页签，可查看集群版本。

        方式二：

        用户还可以通过配置maven仓库的方式下载SDK包。单击“Maven项目依赖“，进入以下页面：

        **图 2**  Maven页面<a name="fig13562256111919"></a>  
        ![](figures/Maven页面.png "Maven页面")

        在[图2](#fig13562256111919)所示的列表中，第一列代表集群版本号，第二列代表GaussDB\(DWS\)  JDBC驱动包的版本号，请根据集群版本号，选择相应版本的驱动包，然后进入以下页面：

        **图 3**  Maven项目依赖<a name="fig101154223208"></a>  
        ![](figures/Maven项目依赖.png "Maven项目依赖")

        复制Maven库信息，并将其添加到pom.xml文件中。例如，在pom.xml文件中添加如下代码配置：

        -   gsjdbc4.jar

            ```
            <dependency>
                <groupId>com.huaweicloud.dws </groupId>
                <artifactId>huaweicloud-dws-jdbc</artifactId>
                <version>8.1.0</version> 
            </dependency>
            ```

        -   gsjdbc200.jar

            ```
            <dependency>
                <groupId>com.huaweicloud.dws</groupId>
                <artifactId>huaweicloud-dws-jdbc</artifactId>
                <version>8.1.1.1-200</version>
            </dependency>  
            ```

    -   **ODBC驱动**

        选择相应的版本，然后单击“下载“可以下载与集群版本匹配的ODBC驱动。如果同时拥有不同版本的集群，单击“下载”时会下载与集群最低版本相对应的ODBC驱动。如果当前没有集群，单击“下载”时将下载到低版本的ODBC驱动。GaussDB\(DWS\) 集群可向下兼容低版本的ODBC驱动。

        单击“历史版本”可根据操作系统和集群版本下载相应版本的ODBC驱动，建议按集群版本进行下载。

        ODBC驱动支持在以下系统中使用：

        -   “Microsoft Windows x86\_64”驱动支持在以下系统中使用：
            -   Windows 7及以上。
            -   Windows Server 2008及以上。

        -   “Euler Kunpeng\_64”驱动支持在以下系统中使用：
            -   EulerOS 2.8。

        -   “Redhat\_Kunpeng\_64”驱动支持在以下系统中使用：
            -   CentOS 7.5,7.6
            -   NeoKylin 7.6

        -   ”Redhat x86\_64”驱动支持在以下系统中使用：
            -   RHEL 6.4\~7.6。
            -   CentOS 6.4\~7.4。
            -   EulerOS 2.3。

        -   ”SUSE x86\_64”驱动支持在以下系统中使用：
            -   SLES 11.1\~11.4。
            -   SLES 12.0\~12.3。

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >Windows驱动只支持32位版本，可以在32或64位操作系统使用，但是应用程序必须为32位。



