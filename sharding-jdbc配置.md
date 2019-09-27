1. 数据库主从分离配置

   - 1.1pom文件中增加依赖

   ```xml
   <dependency>
       <groupId>org.apache.shardingsphere</groupId>
       <artifactId>sharding-jdbc-spring-boot-starter</artifactId>
       <version>4.0.0-RC2</version>
   </dependency>
   <dependency>
       <groupId>org.apache.shardingsphere</groupId>
       <artifactId>sharding-jdbc-spring-namespace</artifactId>
       <version>4.0.0-RC2</version>
   </dependency>
   ```

   - 1.2application.properties中增加配置

   ```properties
   spring.shardingsphere.datasource.names=master,slave0,slave1
   spring.shardingsphere.datasource.master.type=com.zaxxer.hikari.HikariDataSource
   spring.shardingsphere.datasource.master.driver-class-name=com.mysql.cj.jdbc.Driver
   spring.shardingsphere.datasource.master.jdbc-url=jdbc:mysql://192.168.1.41:3306/user?serverTimezone=UTC&characterEncoding=UTF8
   spring.shardingsphere.datasource.master.username=root
   spring.shardingsphere.datasource.master.password=123456
   spring.shardingsphere.datasource.master.maximum-pool-size=10
   
   spring.shardingsphere.datasource.slave0.type=com.zaxxer.hikari.HikariDataSource
   spring.shardingsphere.datasource.slave0.driver-class-name=com.mysql.cj.jdbc.Driver
   spring.shardingsphere.datasource.slave0.jdbc-url=jdbc:mysql://192.168.1.43:3306/user?serverTimezone=UTC&characterEncoding=UTF8
   spring.shardingsphere.datasource.slave0.username=root
   spring.shardingsphere.datasource.slave0.password=123456
   spring.shardingsphere.datasource.slave0.maximum-pool-size=10
   
   spring.shardingsphere.datasource.slave1.type=com.zaxxer.hikari.HikariDataSource
   spring.shardingsphere.datasource.slave1.driver-class-name=com.mysql.cj.jdbc.Driver
   spring.shardingsphere.datasource.slave1.jdbc-url=jdbc:mysql://192.168.1.44:3306/user?serverTimezone=UTC&characterEncoding=UTF8
   spring.shardingsphere.datasource.slave1.username=root
   spring.shardingsphere.datasource.slave1.password=123456
   spring.shardingsphere.datasource.slave1.maximum-pool-size=10
   
   spring.shardingsphere.masterslave.name=ms
   spring.shardingsphere.masterslave.master-data-source-name=master
   spring.shardingsphere.masterslave.slave-data-source-names=slave0,slave1
   spring.shardingsphere.masterslave.load-balance-algorithm-type=round_robin
   ```

   - 1.3新建配置类 ShardingJDBCConfig.java

   ```java
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.context.annotation.Configuration;
   
   import javax.sql.DataSource;
   
   @Configuration
   public class ShardJDBCConfig {
       @Autowired
       private DataSource dataSource;
   }
   
   ```
