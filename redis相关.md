1. redis安装

   - 下载，解压

   ```shell
   tar -zxvf redisxxx -C /user/local
   ```

   - 进入解压后的目录，执行make编译

   ```shell
   cd /usr/local/redis
   make
   ```

   - 删除无用文件，只留下redis下src目录中可执行二进制文件和redis.conf文件

2. 启动redis

   ```shell
   cd /usr/local/redis/src
   ./redis-server
   ```

3. 

