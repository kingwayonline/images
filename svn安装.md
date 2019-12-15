1. 安装svnServer

   ```shell
   yum install subversion
   ```

2. 检查svn是否安装成功

   ```shell
   svnserve --version
   ```

3. 新建svn目录

   ```shell
   mkdir -p /usr/local/svn/repositories
   ```

4. 初始化svn

   ```shell
   svnadmin create /opt/svn/repositories
   ```

5. 配置用户名和密码及权限

   ```shell
   cd conf
   vim passwd
   liubo = 123456
   vim authz
   [/] # 代表根目录下的所有资源
   liubo = rw
   ```

6. 服务svnserve.conf配置

   ```shell
   放开如下注释
   anon-access = read
   auth-access = write
   password-db = passwd
   authz-db = authz
   realm = My First Repository
   ```

7. 启动svnserver

   ```shell
   svnserve -d -r /usr/local/svn/repositories/
   ```

8. 停止svn

   ```shell
   killall svnserve
   ```


