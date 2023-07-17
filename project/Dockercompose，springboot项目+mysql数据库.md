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

url改成容器的url，不然项目访问不到数据库

```
spring.datasource.url=jdbc:mysql://mysql:3306/xxl_job?useSSL=false&characterEncoding=utf8
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
```

