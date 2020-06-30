1. 导入脚本conf/nacos-mysql.sql

2. 修改conf/application.properties

   ```properties
   # 表明用MySQL作为后端存储
   spring.datasource.platform=mysql
   
   # 有几个数据库实例
   db.num=2
   
   # 第1个实例的地址
   db.url.0=jdbc:mysql://11.162.196.16:3306/nacos_devtest?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true
   # 第2个实例的地址
   db.url.1=jdbc:mysql://11.163.152.9:3306/nacos_devtest?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true
   db.user=nacos_devtest
   db.password=nacos
   
   ```


3. 对于mysql8.0

   Nacos 1.0.1内置的connector是 `mysql-connector-java-5.1.34` ，该connector无法连MySQL 8.0。还好Nacos提供了插件机制，可以支持MySQL 8.0+。方法如下：

   - 在上面操作的基础上，下载支持MySQL 8.0的connector，例如：`mysql-connector-java-8.0.16` 。下载地址：[点我下载](https://repo1.maven.org/maven2/mysql/mysql-connector-java/8.0.16/mysql-connector-java-8.0.16.jar)
   - 在Nacos的 `plugins` 目录下创建 `mysql` 目录，并将下载的connector扔到该目录即可。


4. 启动三台nacos

   ```shell
   sh start.sh
   ```


5. 配置nginx

   ```shell
   upstream nacos {
     server 127.0.0.1:8848;
     server 127.0.0.1:8849;
     server 127.0.0.1:8850;
   }
   
   server {
     listen 80;
     server_name  localhost;
     location /nacos/ {
       proxy_pass http://nacos/nacos/;
     }
   }
   ```

6. 重新加载nginx配置文件

   ```
   cd ./nginx -s reload
   ```


