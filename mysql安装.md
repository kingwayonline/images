1. 下载mysql官方二进制安装包，tar.xz文件，下载地址:www.mysql.com，下载到/usr/local/src

2. 解压文件

   ```shell
   tar -xvf xxx.tar.xz -C /usr/local/
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
   bin/mysqld --initialize --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data
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
    skip-grant-tables ## 免密登录
    ```
