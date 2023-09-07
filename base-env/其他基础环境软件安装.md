# 其他基础环境软件安装
## postgreSql



```
docker run -it --name postgre12  -e TZ='Asia/Shanghai' -e POSTGRES_PASSWORD='root' -e ALLOW_IP_RANGE=0.0.0.0/0 -v /home/postgres/data:/var/lib/postgresql -p 5432:5432 -d postgres
```



## Nginx



```
nginx# 创建挂载目录
mkdir -p /home/nginx/conf
mkdir -p /home/nginx/log
mkdir -p /home/nginx/html
mkdir -p  /home/file/attachment/

# 生成容器
docker run --name nginx -p 9001:80 -d nginx
# 将容器nginx.conf文件复制到宿主机
docker cp nginx:/etc/nginx/nginx.conf /home/nginx/conf/nginx.conf
# 将容器conf.d文件夹下内容复制到宿主机
docker cp nginx:/etc/nginx/conf.d /home/nginx/conf/conf.d
# 将容器中的html文件夹复制到宿主机
docker cp nginx:/usr/share/nginx/html /home/nginx/


docker run \
-p 9002:80 \
--name nginx2 \
-v /home/nginx/conf/nginx.conf:/etc/nginx/nginx.conf \
-v /home/nginx/conf/conf.d:/etc/nginx/conf.d \
-v /home/nginx/log:/var/log/nginx \
-v /home/nginx/html:/usr/share/nginx/html \
-v /tmp/bussiness/attachment:/usr/local/business/attachment \
-d nginx:1.16.1
```

## Redis
- **-v**  /home/redis/myredis/myredis.conf:/etc/redis/redis.conf 这里是将 liunx 路径下的myredis.conf 和redis下的redis.conf 挂载在一起。
- **--restart=always** 总是开机启动
- **redis-server /etc/redis/redis.conf** 以配置文件启动redis，加载容器内的conf文件，最终找到的是挂载的目录，`/etc/redis/redis.conf` 也**就是liunx下的/home/redis/myredis/myredis.conf**
- **-d redis** 表示后台启动名称为redis的镜像
- **–requirepass 000415** 设置密码 (可以不设置)

```
docker pull redis

docker run --restart=always -p 6379:6379 --name myredis -v /home/redis/myredis/myredis.conf:/etc/redis/redis.conf -v /home/redis/myredis/data:/data -d redis redis-server /etc/redis/redis.conf  --appendonly yes  --requirepass 000415

```

