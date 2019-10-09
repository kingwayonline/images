1. 引入maven

   ```xml
        <dependency>
            <groupId>org.redisson</groupId>
            <artifactId>redisson-spring-boot-starter</artifactId>
            <version>3.11.3</version>
        </dependency>
   ```


2. 增加配置（主配置文件）

   ```yaml
     redis:
       redisson:
         config: classpath:redisson.yaml				
   ```

   或者

   ```properties
   spring.redis.redisson.config=classpath:redisson.yaml
   ```



3. 新建redisson.yaml文件

   ```yaml
   masterSlaveServersConfig:
     idleConnectionTimeout: 10000 #连接空闲超时，单位：毫秒
     pingTimeout: 1000
     connectTimeout: 10000 #同任何节点建立连接时的等待超时。时间单位是毫秒。
     timeout: 3000 #命令等待超时，单位：毫秒
     retryAttempts: 3 #命令失败重试次数
     retryInterval: 1500  #命令重试发送时间间隔，单位：毫秒
     reconnectionTimeout: 3000 #重新连接时间间隔，单位：毫秒
     failedAttempts: 3 #执行失败最大次数
     password: 123456 #用于节点身份验证的密码
     subscriptionsPerConnection: 5 #单个连接最大订阅数量
     clientName: user-center #在Redis节点里显示的客户端名称
     loadBalancer: !<org.redisson.connection.balancer.RoundRobinLoadBalancer> {}
     #负载均衡算法类的选择
     #org.redisson.connection.balancer.WeightedRoundRobinBalancer - 权重轮询调度算法
     #org.redisson.connection.balancer.RoundRobinLoadBalancer - 轮询调度算法
     #org.redisson.connection.balancer.RandomLoadBalancer - 随机调度算法
     slaveSubscriptionConnectionMinimumIdleSize: 1
     slaveSubscriptionConnectionPoolSize: 50
     slaveConnectionMinimumIdleSize: 32 #从节点最小空闲连接数
     slaveConnectionPoolSize: 64 #多从节点的环境里，每个 从服务节点里用于普通操作（非 发布和订阅）连接的连接池最大容量。连接池的连接数量自动弹性伸缩。
     masterConnectionMinimumIdleSize: 32 #主节点最小空闲连接数
     masterConnectionPoolSize: 64 #主节点的连接池最大容量。连接池的连接数量自动弹性伸缩。
     readMode: "SLAVE" #读取操作的负载均衡模式，
     #默认值： SLAVE（只在从服务节点里读取）
     #设置读取操作选择节点的模式。
     #可用值为：
     #SLAVE - 只在从服务节点里读取。
     #MASTER - 只在主服务节点里读取。
     #MASTER_SLAVE - 在主从服务节点里都可以读取。
     slaveAddresses:
     - "redis://192.168.1.43:6379"
     - "redis://192.168.1.44:6379"
     masterAddress: "redis://192.168.1.41:6379"
     #主节点地址，可以通过host:port的格式来指定主节点地址。
     database: 0
   threads: 0   # 线程池数量
   #默认值: 当前处理核数量 * 2
   #这个线程池数量被所有RTopic对象监听器，RRemoteService调用者和RExecutorService任务共同共享。
   nettyThreads: 0
   codec: !<org.redisson.codec.JsonJacksonCodec> {}    # 编码
   #默认值: org.redisson.codec.JsonJacksonCodec
   transportMode: "NIO"    # 传输模式，默认值：TransportMode.NIO
   #TransportMode.NIO,
   #TransportMode.EPOLL
   #TransportMode.KQUEUE
   ```



4. 通过RedisTemplate使用redisson

   ```java
   @Autowired
   private RedisTemplate<String,String> redisTemplate;
   ```


