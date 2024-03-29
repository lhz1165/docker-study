# docker-study
## mysql环境

### mysql5.7 （端口为3306）

```properties
spring.datasource.url = jdbc:mysql://127.0.0.1:3306/wiki?useSSL=false&characterEncoding=utf8
spring.datasource.username = root
spring.datasource.password = root
spring.datasource.driverClassName = com.mysql.jdbc.Driver
```

镜像和容器

**-name** : 容器名称

**-e MYSQL_DATABASE**  创建一个基础库(可以不写)

**docker.io/mysql:5.7** ==> 镜像名:TAG标签

**-v** 容器与宿主机绑定一个卷

docker.io/mysql 官方镜像

5.7 TAG标签

```shell
docker pull mysql:5.7

docker update mysql --restart=always

docker run \
-p 3306:3306 \
--name mysql57 \
-v ~/mysql/data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=root \
-e MYSQL_DATABASE=blog \
--privileged=true \
docker.io/mysql:5.7

```

### mysql8(修改端口为3307)

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/bim?serverTimezone=Asia/Shanghai&autoReconnect=true&autoReconnect=true&useSSL=false&characterEncoding=utf8
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

镜像和容器

```
docker pull mysql:8.0.32

// 安装msyql8 并且设置端口为3307
docker run -it -d --name mysql8 \
-p 3307:3307 \
-v /mydata2/mysql/log:/var/log/mysql \
-v /mydata2/mysql/data:/var/lib/mysql \
-v /mydata2/mysql/conf:/etc/mysql/conf.d \
-e MYSQL_ROOT_PASSWORD=root \
-e TZ=Asia/Shanghai \
--privileged=true  \
docker.io/mysql:8.0.32

/进入容器 支持远程连接
mysql -P3307 -u root -p
//一. 解决host不受限制
//1. 授予指定用户 'root'@'%' 对所有数据库和所有表的所有权限，并设置密码为 '12345'，同时允许该用户将权限授予其他用户
//GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '{password}' WITH GRANT OPTION;
//2. 授予指定用户 'root'@'%' 对所有数据库和所有表的所有权限 表示host不受限制。上面的可能有问题
//grant all privileges on *.* to 'root'@'%';

//二.
//修改密码加密方式
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'root';

//刷新
flush privileges;

//去在/etc/mysql/conf.d或者/etc/my.cnf 增加或者修改mysqld的配置
[mysqld]
port=3307

```

