# Dockercompose，springboot项目+mysql数据库

构建xxljob的dockerFile

```dockerfile
FROM openjdk:8-jre-slim
MAINTAINER xuxueli2

ENV PARAMS=""

ENV TZ=PRC
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

#把打包后的jar复制到docker容器里的/app.jar
ADD target/xxl-job-admin-*.jar /app.jar
EXPOSE 8086

ENTRYPOINT ["sh","-c","java -jar $JAVA_OPTS /app.jar $PARAMS"]

```



```dockerfile
# 该镜像需要依赖的基础镜像
FROM openjdk:8-jre-slim
#时区设置
ENV TZ=PRC
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
# 将当前目录下的jar包复制到docker容器的/目录下
ADD target/xxl-job-admin-*.jar /xx-job.jar
# 运行过程中创建一个mall-tiny-docker-file.jar文件
# RUN bash -c 'touch /mall-tiny-docker-file.jar'
# 声明服务运行在8080端口
EXPOSE 8086
# 指定docker容器启动时运行jar包
ENTRYPOINT ["java", "-jar","/xx-job.jar"]
# 指定维护者的名字
MAINTAINER lhz
```



构建docker-compose.yml

```dockerfile
version: '3'
services:
  web:
    build: .
    container_name: myxxjob
    restart: always
    ports:
      - "8086:8086"
    depends_on:
      - mysql
 ##docker的容器名称 springbooturl 必须写这个地址
  mysql:
    image: mysql:5.7
    #容器名称
    container_name: mysql5_7  
    #允许外部访问
    command: --default-authentication-plugin=mysql_native_password
    ports:
      - "3306:3306"
    restart: always
    volumes:
    #这里如果之前有mysql挂在过，那么填之前的volumes，数据还存在
      - ~/mysql/data:/var/lib/mysql
    environment:
      MYSQL_DATABASE: xxl_job #创建一个初始的空数据库，名为webserver
      MYSQL_ROOT_USER: root #root用户
      MYSQL_ROOT_PASSWORD: root #root密码
      MYSQL_ROOT_HOST: '%'
      TZ: Asia/Shanghai #时区


```

修改配置文件

url改成mysql容器的名称，不然项目访问不到数据库

```
spring.datasource.url=jdbc:mysql://mysql:3306/xxl_job?useSSL=false&characterEncoding=utf8
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
```

输入命令

```
启动
docker-compose up -d
```

