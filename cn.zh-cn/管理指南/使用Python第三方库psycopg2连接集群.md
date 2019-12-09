# 使用Python第三方库psycopg2连接集群<a name="dws_01_0120"></a>

用户在创建好数据仓库集群后使用psycopg2第三方库连接到集群，则可以使用Python访问DWS，并进行数据表的各类操作。

## 连接集群前的准备<a name="section5781841515252"></a>

-   DWS集群已绑定弹性IP。
-   已获取DWS集群的数据库管理员用户名和密码。
-   已获取DWS集群的公网访问地址，含IP地址和端口。具体请参见[获取集群连接地址](获取集群连接地址.md)。
-   已安装psycopg2第三方库。下载地址：[https://pypi.org/project/psycopg2/](https://pypi.org/project/psycopg2/)

## 在Linux环境使用psycopg2第三方库连接集群<a name="section2825650154610"></a>

1.  以**root**用户登录Linux环境。
2.  执行以下命令创建python\_dws.py文件，并把复制粘贴以下内容放进入python\_dws.py文件。

    **vi python\_dws.py**

    ```
    #!/usr/bin/python
    # -*- coding: UTF-8 -*- 
    
    import psycopg2
    def CreateTable(connection):
        print "Begin to create table"
        try:
            cursor = connection.cursor()
            cursor.execute('''drop table if exists test;create table test(id int, name text);''')
            #print "Table created successfully"
            connection.commit()
        except psycopg2.ProgrammingError,e:
            print e
        else:
            print "Table created successfully"
            cursor.close()
    
    
    def InsertData(connection):
        print "Begin to insert data"
        try:
            cursor = connection.cursor()
            cursor.execute("insert into test values(1,'number1');")
            cursor.execute("insert into test values(2,'number2');")
            cursor.execute("insert into test values(3,'number3');")
            connection.commit()
        except psycopg2.ProgrammingError,e:
            print e
        else:
            print "Insert data successfully"
            cursor.close()
    
    
    def UpdateData(connection):
        print "Begin to update data"
        try:
            cursor = connection.cursor()
            cursor.execute("update test set name = 'numberupdated' where id=1;")
            connection.commit()
            print "Total number of rows updated :", cursor.rowcount
            cursor.execute("select * from test;")
            rows=cursor.fetchall()
            for row in rows:
                print "id = ", row[0]
                print "name = ", row[1], "\n"
        except psycopg2.ProgrammingError,e:
            print e
        else:
            print "After Update, Operation done successfully";
    
    
    def DeleteData(connection):
        print "Begin to delete data"
        try:
            cursor = connection.cursor()
            cursor.execute("delete from test where id=3;")
            connection.commit()
            print "Total number of rows deleted :", cursor.rowcount
            cursor.execute("select * from test;")
            rows=cursor.fetchall()
            for row in rows:
                print "id = ", row[0]
                print "name = ", row[1], "\n"
        except psycopg2.ProgrammingError,e:
            print e
        else:
            print "After Delete,Operation done successfully";
    
    
    def SelectData(connection):
        print "Begin to select data"
        try:
            cursor = connection.cursor()
            cursor.execute("select * from test;")
            rows=cursor.fetchall()
            for row in rows:
                print "id = ", row[0]
                print "name = ", row[1], "\n"
        except psycopg2.ProgrammingError,e:
            print e
            print "select failed"
        else:
            print "Operation done successfully";
            cursor.close()
    
    if __name__ == '__main__':
        try:
            connection = psycopg2.connect(host='10.154.70.231', port='8000', database='postgres', user='dbadmin', password='Bigdata_2013')
        except psycopg2.DatabaseError, e:
            print e
            print "Connect database failed"
        else:
            print "Opened database successfully"
            CreateTable(connection)
            InsertData(connection)
            SelectData(connection)
            UpdateData(connection)
            DeleteData(connection)
            connection.close()
    ```

3.  按照实际集群信息，修改python\_dws.py文件中的集群公网访问地址、集群端口号、数据库名称、数据库用户名、数据库密码。

    psycopg2接口不提供重试连接的能力，您需要在业务代码中实现重试处理。

    ```
    connection = psycopg2.connect(host='10.154.70.231', port='8000', database='postgres', user='dbadmin', password='Bigdata_2013')
    ```

4.  执行以下命令，使用psycopg第三方库连接集群。

    **python python\_dws.py**


## 在Windows环境使用psycopg2第三方库连接集群<a name="section79862501183"></a>

1.  在Windows系统中，单击“开始“按钮 ，在搜索框中，键入**cmd**，然后在结果列表中单击“cmd.exe”打开命令提示符窗口。
2.  在命令提示符窗口中，执行以下命令创建python\_dws.py文件，并把复制粘贴以下内容放进入python\_dws.py文件。

    ****type nul\>**  python\_dws.py**

    ```
    #!/usr/bin/python
    # -*- coding: UTF-8 -*-
    
    import psycopg2
    def CreateTable(connection):
        print "Begin to create table"
        try:
            cursor = connection.cursor()
            cursor.execute('''drop table if exists test;create table test(id int, name text);''')
            #print "Table created successfully"
            connection.commit()
        except psycopg2.ProgrammingError,e:
            print e
        else:
            print "Table created successfully"
            cursor.close()
    
    
    def InsertData(connection):
        print "Begin to insert data"
        try:
            cursor = connection.cursor()
            cursor.execute("insert into test values(1,'number1');")
            cursor.execute("insert into test values(2,'number2');")
            cursor.execute("insert into test values(3,'number3');")
            connection.commit()
        except psycopg2.ProgrammingError,e:
            print e
        else:
            print "Insert data successfully"
            cursor.close()
    
    
    def UpdateData(connection):
        print "Begin to update data"
        try:
            cursor = connection.cursor()
            cursor.execute("update test set name = 'numberupdated' where id=1;")
            connection.commit()
            print "Total number of rows updated :", cursor.rowcount
            cursor.execute("select * from test;")
            rows=cursor.fetchall()
            for row in rows:
                print "id = ", row[0]
                print "name = ", row[1], "\n"
        except psycopg2.ProgrammingError,e:
            print e
        else:
            print "After Update, Operation done successfully";
    
    
    def DeleteData(connection):
        print "Begin to delete data"
        try:
            cursor = connection.cursor()
            cursor.execute("delete from test where id=3;")
            connection.commit()
            print "Total number of rows deleted :", cursor.rowcount
            cursor.execute("select * from test;")
            rows=cursor.fetchall()
            for row in rows:
                print "id = ", row[0]
                print "name = ", row[1], "\n"
        except psycopg2.ProgrammingError,e:
            print e
        else:
            print "After Delete,Operation done successfully";
    
    
    def SelectData(connection):
        print "Begin to select data"
        try:
            cursor = connection.cursor()
            cursor.execute("select * from test;")
            rows=cursor.fetchall()
            for row in rows:
                print "id = ", row[0]
                print "name = ", row[1], "\n"
        except psycopg2.ProgrammingError,e:
            print e
            print "select failed"
        else:
            print "Operation done successfully";
            cursor.close()
    
    if __name__ == '__main__':
        try:
            connection = psycopg2.connect(host='10.154.70.231', port='8000', database='postgres', user='dbadmin', password='Bigdata_2013')
        except psycopg2.DatabaseError, e:
            print e
            print "Connect database failed"
        else:
            print "Opened database successfully"
            CreateTable(connection)
            InsertData(connection)
            SelectData(connection)
            UpdateData(connection)
            DeleteData(connection)
            connection.close()
    ```

3.  按照实际集群信息，修改python\_dws.py文件中的集群公网访问地址、集群端口号、数据库名称、数据库用户名、数据库密码。

    ```
    connection = psycopg2.connect(host='10.154.70.231', port='8000', database='postgres', user='dbadmin', password='Bigdata_2013')
    ```

4.  在命令提示符窗口中，执行以下命令，使用psycopg第三方库连接集群。

    **python python\_dws.py**


