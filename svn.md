1. 建立目录

   ```shell
   yum -y install subversion
   svnserve --version
   mkdir /usr/local/svn/repositories
   svnadmin create /usr/local/svn/repositories
   vim svnserve.conf
   ## 打开注释
   anon-access = read
   auth-access = write
   password-db = passwd
   authz-db = authz
   realm = My First Repository
   vim authz ##添加人员
   ## 在最后添加
   [/]
   liubo = rw
   zhengmenglong = rw
   daqiang = rw
   vim passwd ## 配置密码
   liubo = liubo
   xiesongshan = xiesongshan
   tianquanhao = tianquanhao
   peizhiqiang= peizhiqiang
   xuewenjie = xuewenjie                   
   svnserve -d -r /usr/local/svn/repositories ## 启动svn
   ```
