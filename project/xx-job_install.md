# 1.xxjob 和mysql 容器单独运行

拉取xxjob代码

-t 表示指定 【镜像仓库名称】/【镜像名称】:【镜像标签】 【.】表示使用当前目录下的Dockerfile

使用当前目录的 Dockerfile 创建镜像，标签为 xxjob/xxjob:0.0.1

**镜像名称** xxjob/xxjob

**tag版本** 0.0.1

. 代表当前目录下

```
docker build -t xxjob/xxjob:0.0.1 .
```

运行（连接mysql容器）

```
// 1.首先根据容器名(mysql57) 称查询容器的ip
docker  inspect  mysql57 | grep IP

// 2. 修改xxjob代码里面的数据库ip为容器ip


//3. 启动容器，使用--link连接mysql容器
//--link mysql57:mysql557 -d xxjob/xxjob:0.0.1
//--link 容器名称:别名 -d 镜像名称

docker run -p 8080:8080 -v /tmp:/data/applogs --name xxjob --link mysql57:mysql557 -d xxjob/xxjob:0.0.1
```

