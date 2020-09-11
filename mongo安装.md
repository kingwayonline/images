1. 下载mongo

```shell
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-4.4.0.tgz
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-4.0.19.tgz
tar -zxvf mongodb-linux-x86_64-rhel70-4.4.0.tgz -C /usr/local
mv mongodb-linux-x86_64-rhel70-4.4.0 mongo
```

2. 新建数据和日志目录

```shell
mkdir data
mkdir log
```

3. 新建mongo.conf配置文件

```yaml
systemLog:
  destination: file
  path: /usr/local/mongo/log/mongo.log
  logAppend: true
storage:
  dbPath: /usr/local/mongo/data
  journal:
    enabled: true
net:
  bindIp: 0.0.0.0
  port: 27017
replication:
  replSetName: myrs
processManagement:
  fork: true
```

4. 添加环境变量

```shell
export PATH=$PATH:$JAVA_HOME/bin:/usr/local/mongo/bin
source /etc/profile
```

5. 启动mongo

```shell
bin/mongod -f mongo.conf 
```

6. 复制集配置

```
rs.initiate()
rs.initiate({_id:'myrs',members:[{_id:0,host:'10.10.10.4:27017'}]}) 
rs.add("ip:port")
rs.add("ip:port")
```

7. 在从节点执行

```shell
rs.slaveOk()
# 修改host
var config = rs.config();
config.members[0].host = "想要设置的ip：27017";
rs.reconfig(config)
```

