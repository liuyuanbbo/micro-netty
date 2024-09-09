# 拉取docker镜像

```
docker pull mysql:8.0.39
```

# 创建宿主机 mysql 挂载目录

```
mkdir -p /opt/mydata/mysql/data /opt/mydata/mysql/log /opt/mydata/mysql/conf
```

# 创建 my.cnf

```
touch /opt/mydata/mysql/conf/my.cnf
vim /opt/mydata/mysql/conf/my.cnf
```

```
[client]
default-character-set=utf8mb4

[mysql]
default-character-set=utf8mb4
[mysqld]
init_connect='SET collation_connection = utf8mb4_general_ci'
init_connect='SET NAMES utf8mb4'
character-set-server=utf8mb4
collation-server=utf8mb4_general_ci
skip-character-set-client-handshake
skip-name-resolve
```

# 运行 mysql 容器

```
docker run -p 3336:3336 --name mysql \
-v /opt/mydata/mysql/log:/var/log/mysql \
-v /opt/mydata/mysql/data:/var/lib/mysql \
-v /opt/mydata/mysql/conf:/etc/mysql/conf.d \
-v /opt/mydata/mysql/mysql-files:/var/lib/mysql-files \
-e MYSQL_ROOT_PASSWORD=123456 \
-d mysql:8.0.39
```

# 拉取镜像

```
docker pull redis:7.4.0
```

# 创建配置文件

```
mkdir -p /opt/mydata/redis/conf
touch /opt/mydata/redis/conf/redis.conf
vim /opt/mydata/redis/conf/redis.conf
```

```
appendonly yes
requirepass 123456
port 6380
```

# 运行容器

```
docker run -p 6380:6380 --name rds0 \
-v /opt/mydata/redis/data:/data \
-v /opt/mydata/redis/conf/redis.conf:/etc/redis/redis.conf \
-d redis:7.4.0 redis-server /etc/redis/redis.conf
```