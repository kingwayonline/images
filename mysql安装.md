1. 下载mysql官方二进制安装包，tar.xz文件，下载地址:www.mysql.com，下载到/usr/local/src

2. 解压文件

   ```shell
   tar -xvf xxx.tar.xz -C /usr/local/
   # 删除mariadb
   rpm -qa|grep mariadb  
   yum remove mysql mysql-server mysql-libs compat-mysql51
   yum remove mariadb
   rm -rf /etc/my.cnf
   rm -rf /etc/my.cnf.d
   ```

3. 改名

   ```shell
   mv mysqlxxxx mysql
   ```

4. 新建用户及用户组(必须新建否则无法启动)

   ```shell
   groupadd mysql
   useradd -r -g mysql -s /bin/false mysql
   ```

5. 初始化mysql，并记住root用户初始化密码

   ```shell
   yum install libaio
   yum -y install numactl
   bin/mysqld --initialize --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data --lower-case-table-names=1
   ```

6. mysql启动停止

   ```shell
   bin/mysqld_safe --user=mysql &
   ./mysql.server start
   ./mysql.server stop
   ./mysql.server restart
   ```

7. 登录mysql

   ```shell
   bin/mysql -uroot -p
   密码为初始化记录的密码
   ```

8. 修改root密码

   ```sql
   ALTER user 'root'@'localhost' IDENTIFIED BY '123456';
   ```

9. 修改加密方式

   ```sql
   use mysql;
   update user set plugin='mysql_native_password' where user='root';
   flush privileges;
   update user set authentication_string='' where user='root'; --更新密码为空
   quit --退出重新登录
   bin/mysql -uroot -p --没有密码直接回车登录
   ALTER user 'root'@'localhost' IDENTIFIED BY '123456';
   ```

10. 修改可以远程登录

    ```sql
       select user,host,plugin from user;   //查看用户是否开启远程
       update user set host='%' where user='root';
       flush privileges;
    ```

11. 忘记密码，新建my.cnf 放到/etc目录下。重启mysql

    ```shell
    [mysqld]
    basedir=/usr/local/mysql
    datadir=/usr/local/mysql/data
    max_connections=1000
    lower_case_table_names=1 ## 表名不区分大小写
    skip-grant-tables ## 免密登录
    ```

12. mysql集群配置

    ```shell
    新建my.cnf文件，增加如下内容
    主机：
    server-id=1 ##（必须）
    log-bin=/usr/local/mysql/data/mysqlbin ##（必须）
    log-error=/usr/local/mysql/data/mysqlerr ##（不必须）
    tmpdir=/usr/local/mysql/tmp ##（不必须）
    read-only=0 ##可读可写
    binlog-ignore-db=mysql ##设置不需要复制的数据库
    ## binlog-do-db= 设置需要复制的数据库
    从机：
    basedir=/usr/local/mysql
    datadir=/usr/local/mysql/data
    server-id=2
    log-bin=/usr/local/mysql/data/mysqlbin
    log-error=/usr/local/mysql/data/mysqlerr
    重启服务器，加载my.cnf文件
    ```

    ```sql
    -- 主机操作
    create user 'slave1'@'%' identified  WITH mysql_native_password by '123456';
    grant replication slave on *.* to 'slave1'@'%' ;
    flush privileges;
    show master status;
    -- 记录File和Position
    -- File:mysqlbin.000002
    -- Position:1317
    ```

    ```sql
    -- 从机操作
    change master to
    master_host='192.168.1.41', --主机ip
    master_user='slave1',
    master_password='123456',
    master_log_file='mysqlbin.000002',
    master_log_pos=1317;
    flush privileges;
    start slave;
    -- stop slave;
    --reset slave;
    show slave status\G; -- 查看从机状态
    -- Slave_IO_Running: Yes  必须是yes
    -- Slave_SQL_Running: Yes  必须是yes                           
    ```
13. 安装mysql客户端
    ```shell
    yum install mysql  -y
    ```
